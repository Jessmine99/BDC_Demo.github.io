---
title: Salesforce Ingestion & Medallion Pipeline
layout: default
nav_order: 4
---

# Salesforce Ingestion & Medallion Pipeline

Log in SAP Databricks. From `product switch` icon (top right corner) next to your username icon choose `SAP Databricks`

## Data Ingestion (Bronze Layer - Raw Data)
- Click on `+New` at the top left --> `Add or upload data` --> Choose `EU_Accounts` csv file.  
- In the catalog, choose `hana_cloud_dbx_catalog` and for the schema choose `bronze`  
- Click on `Create Table`  

---

## Data Modeling (Silver - Gold Layer)
- Workspace --> Users --> Click on your username --> Click on the 3 vertical dots next to `Share` on top right corner --> `Import` --> `EU_Accounts (Data Modeling)` notebook  
- Open the notebook and run the code  
- A refined table with key attributes and defined data types is created  

## Delta Sharing
- Catalog --> `hana_cloud_dbx_catalog` --> `gold` schema --> `eu_accounts`  
- Select `Share` on the top right corner --> `Share via Delta Sharing` --> Create a new share with a view  
- Share name: `EU_Accounts_(your Username)` --> Recipient: `Business Data Cloud` 

## Publish Data Product
- Workspace --> Users --> Click on your username --> Click on the 3 vertical dots next to `Share` on top right corner --> `Import` --> Import `Publish_Data_Product_EU_Accounts` notebook   
- Open the notebook. From navigation bar on the right --> choose environment `V3`  
- In code block: `share_name = "eu_accounts_yourusername"` **(ensure your username is lowercase)**  
- Run all code blocks  

### Verify Data Product is Published
- Log in to SAP Datasphere  
- Go to `Catalog & Marketplace` and in the search bar type your `share_name`  

{: .note }
It might take a few minutes for the data product to appear 

## Install Data Product

{: .warning }
Not possible due to limitations in SAP workshop environment.
