---
title: Data acquisition and Data Ingestion
layout: default
nav_order: 2
---

# Data acquisition and Data Ingestion

## Log on to Datasphere
Use credentials that are already given to you

## Explore your own space
### Create time dimensions & tables
Navigate to space managemenent. Select the edit button on your assigned space, where your username is displayed. Scroll down in the time section where you can generate time data for your space. Click edit on time data. When you update the year range, this will generate time tables with data and dimension views.

### Preview time dimensions & tables
Select Repository Explorer in the side navigation area. You should see:
4 views of type Dimension
3 local tables of type Text
1 local table of type Relational Dataset

## Data acquisition
Open Data Builder on your space. Navigate to Data Builder and select your space.

### Create Sales Order local Table
1️⃣ In Data Builder, create a new table. Enter Business Name / Technical Name as `Sales Order`.

2️⃣ Add all required columns and assign appropriate data types.

![Attributes](https://raw.githubusercontent.com/Jessmine99/BDC_Demo.github.io/main/images/Sales%20Order%20Local%20Table%201.png)

![Attributes](https://raw.githubusercontent.com/Jessmine99/BDC_Demo.github.io/main/images/Sales%20Order%20Fact%20attributes%202.png)

3️⃣ Mark `DOCUMENT_ID`, `DOCUMENT_ID_POSITION` as **Key Attributes**. 

4️⃣ Click Save and confirm the business/technical name. Then click Deploy to activate the table.

---

### Create Customer local table
1️⃣ In Data Builder, create a new table. Enter Business Name / Technical Name as `Customer`.

2️⃣ Add required columns and define data types.

3️⃣ Mark `CUSTOMER_NUMBER` as the **Key Attribute**.

4️⃣ Click Save and confirm the business/technical name. Then click Deploy to activate the table.

---

### Create Material local table
1️⃣ In Data Builder, create a new table. Enter Business Name / Technical Name as `Material`.

2️⃣ Add required columns and define data types.

3️⃣ Mark `MATERIAL_ID` as the **Key Attribute**.

4️⃣ Click Save and confirm the business/technical name. Then click Deploy to activate the table

---

### Create Distribution Channel table 
*(Later used for modeling the Customer Dimension)*

1️⃣ Go to Data Builder → Create New Table

2️⃣ Name the table: `DISTR_CHANNEL`

Add the following columns:

| Column Name | Data Type |
|-------------|-----------|
| DISTRIBUTION_CHANNEL | String (2) |
| DISTRIBUTION_CHANNEL_NAME | String (10) |
| DELIVERY_CONDITION | String (20) |
| CREDIT_LIMIT | Integer64 |
| LEAD_TIME_DAYS | Integer64 |
| PAYMENT_TERMS | String (10) |

3️⃣ Set `DISTRIBUTION_CHANNEL` as the **Key Attribute**

## Data Ingestion
### Import csv files into the local tables 
1️⃣ Go to data builder and select and open each local table(customer, sales order, material). Choose Upload Data from CSV File icon from the toolbar.
   Select the appropriate file for each local table:
   Customer DIM geo.csv --> Customer
   Sales Order Fact.csv --> Sales Order
   Material DIM.csv --> Material 

2️⃣ In the Import CSV File wizard, verify the settings:
   Ensure the 'Delete Existing Data Before Upload’checkbox is marked
   Ensure the ‘Use first row as column header’ checkbox is marked
   Ensure that all columns of the table have a mapped column from the CSV File

3️⃣ Click on Data viewer from the toolbar to verify data.

4️⃣ Click save and then click deploy.
