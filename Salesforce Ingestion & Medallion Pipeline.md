---
title: 3.Salesforce Ingestion & Medallion Pipeline
layout: default
nav_order: 4
---

# Salesforce Ingestion & Medallion Pipeline

Log in SAP Databricks. From `product switch` icon (top right corner) next to your username icon choose `SAP Databricks`

## Data Ingestion
- Click on `+New` at the top left --> `Add or upload data` --> Choose `EU_Accounts` csv file.  
- In the catalog, choose `workspace` and for the schema choose `default`  
- Click on `Create Table`  

---

## Data Modeling - Medallion pipeline
- Workspace --> Users --> Click on your username --> Click on the 3 vertical dots next to `Share` on top right corner --> `Import` --> `EU_Accounts (Data Modeling)` notebook  
- Open the notebook and run the code  

<p>
  <img
    src="{{ site.baseurl }}/images/medallion architecture.png"
    alt="Medallion architecture"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img1').showModal()"
  >
</p>

<dialog id="img1" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/medallion architecture.png" style="max-width:90vw;">
</dialog>

### Bronze Layer – Raw Data
The Bronze table contains the raw ingested data.This layer stores the original dataset as it was imported from the source system.

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
- This results in an `account_clusters` table 

## Delta Sharing
- Catalog --> `workspace` --> `default` schema --> `eu_accounts_gold`  
- Select `Share` on the top right corner --> `Share via Delta Sharing` --> Create a new share with a view  
- Share name: `account_clusters(your Username)` --> Recipient: `Business Data Cloud` 

## Publish Data Product
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
