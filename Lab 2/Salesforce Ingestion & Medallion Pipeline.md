---
title: 4.Salesforce Ingestion & Medallion Pipeline
layout: default
nav_order: 5
---

# Salesforce Ingestion & Medallion Pipeline

Log in SAP Databricks. From `product switch` icon (top right corner) next to your username icon choose `SAP Databricks`

## SFDC Data Ingestion
- Click on `+New` at the top left --> `Add or upload data` --> Choose `EU_Accounts` xlsx file.  
- In the catalog, choose `workspace` and for the schema choose `default`  
- Click on `Create Table`  

<p>
  <img
    src="{{ site.baseurl }}/images/upload_data_databricks.png"
    alt="upload_data_databricks"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img8').showModal()"
  >
</p>

<dialog id="img8" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/upload_data_databricks.png" style="max-width:90vw;">
</dialog>
---
## Data Modeling - Medallion pipeline

{: .note }
Download the required notebook from the IBM Box folder:
[IBM Lab - “custom” Data Products, Modeling and SAC reporting](https://ibm.ent.box.com/folder/369590392350?s=n5xb24fwnpfk4x0izfeyxyk4b6leuc2t&tc=collab-folder-invite-treatment-b)

- Workspace --> Users --> Click on your username --> Click on the 3 vertical dots next to `Share` on top right corner --> `Import` --> `EU_Accounts (Data Modeling)` notebook  
- Open the notebook and run the code  

<p>
  <img
    src="{{ site.baseurl }}/images/import_workbook.png"
    alt="import_workbook"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img9').showModal()"
  >
</p>

<dialog id="img9" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/import_workbook.png" style="max-width:90vw;">
</dialog>

### Bronze Layer – Raw Data
The Bronze table contains the raw ingested data.This layer stores the original dataset as it was imported from the source system.
<p>
  <img
    src="{{ site.baseurl }}/images/medallion architecture.png"
    alt="Medallion architecture"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img1').showModal()"
  >
</p>

<dialog id="img1" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/medallion architecture.png" style="max-width:90vw;">
</dialog>
### Silver Layer – Data Cleaning & Structuring
In the Silver layer, the data is cleaned and structured:
- Define the key attribute (`Id`)
- Set data types for the columns
- Remove invalid or null records where necessary
- Prepare the dataset for further processing
This results in a refined table: `eu_accounts_silver`.

### Gold Layer – Analytical Dataset
The Gold layer prepares the dataset for analytics and machine learning:
- Copy the structured data from the Silver table
- Add additional attributes such as `CustomerSegment`
- Select the relevant columns required for analysis
- Handle remaining null values
This results in a refined table: `eu_accounts_gold`.

#### Machine Learning Clustering
Using the Gold dataset:
- Relevant features are selected for clustering
- Categorical columns are transformed into numerical values using One-Hot Encoding
- A clustering model (Affinity Propagation) is trained
- Hyperparameters are optimized to find the best clustering configuration
- The resulting clusters are stored and can be visualized in dashboards  
- Additional business attributes such as account type, industry, ERP customer code, and customer segment are added to the result table. This allows the clusters to be analyzed and visualized in SAP Analytics Cloud dashboards.
- This results in an `account_clusters` table. To view the table go to `catalog` --> `workspace` --> `default` --> `tables` --> `account_clusters` 

<p>
  <img
    src="{{ site.baseurl }}/images/account_clusters_1.png"
    alt="account_clusters_1"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img13').showModal()"
  >
</p>

<dialog id="img13" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/account_clusters_1.png" style="max-width:90vw;">
</dialog>

<p>
  <img
    src="{{ site.baseurl }}/images/account_clusters_2.png"
    alt="account_clusters_2"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img14').showModal()"
  >
</p>

<dialog id="img14" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/account_clusters_2.png" style="max-width:90vw;">
</dialog>

## Delta Sharing
- Catalog --> `workspace` --> `default` schema --> `account_clusters`  
- Select `Share` on the top right corner --> `Share via Delta Sharing` --> Create a new share with a view  
- Share name: `account_clusters(your Username)` --> Recipient: `Business Data Cloud` 

## Publish Data Product

{: .note }
Download the required notebook from the IBM Box folder:
[IBM Lab - “custom” Data Products, Modeling and SAC reporting](https://ibm.ent.box.com/folder/369590392350?s=n5xb24fwnpfk4x0izfeyxyk4b6leuc2t&tc=collab-folder-invite-treatment-b)

- Workspace --> Users --> Click on your username --> Click on the 3 vertical dots next to `Share` on top right corner --> `Import` --> Import `Publish_Data_Product_EU_Accounts` notebook   
- Open the notebook. From navigation bar on the right --> choose environment `V3`  
- In code block: `share_name = "account_clusters_yourusername"` **(ensure your username is lowercase)**  
- Run all code blocks  

### Verify Data Product is Published
- Log in to SAP Datasphere  
- Go to `Catalog & Marketplace` and in the search bar type your `share_name`  

{: .note }
It might take a few minutes for the data product to appear 

## Install Data Product

{: .warning }
Not possible due to limitations in SAP workshop environment.

Instead, we manually download the table and later use it to create the dimension view in SAP Datasphere.
Navigate to `Workspace` → `Users` → click on your username → open the `EU_Accounts (Data Modeling)` notebook.  
From the last code block, download the table as a **CSV file**.

<p>
  <img
    src="{{ site.baseurl }}/images/account_clusters_csv.png"
    alt="account_clusters_csv"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img15').showModal()"
  >
</p>

<dialog id="img15" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/account_clusters_csv.png" style="max-width:90vw;">
</dialog>