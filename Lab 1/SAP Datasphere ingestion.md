---
title: 1.SAP Datasphere ingestion
layout: default
nav_order: 2
---

# Ingest S/4HANA CSV Files into SAP Datasphere

## Log on to Datasphere
Use credentials that are already given to you

## Explore your own space
### Create time dimensions & tables

{: .highlight }
Navigate to space managemenent. Select the edit button on your assigned space, where your username is displayed. Scroll down in the time section where you can generate time data for your space. Click edit on time data. When you update the year range, this will generate time tables with data and dimension views.

### Preview time dimensions & tables

{: .highlight }
Select Repository Explorer in the side navigation area. You should see:
4 views of type Dimension
3 local tables of type Text
1 local table of type Relational Dataset

## Data acquisition
Navigate to Data Builder and select your space.

<p>
  <img
    src="{{ site.baseurl }}/images/data_builder.png"
    alt="data_builder"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img1').showModal()"
  >
</p>

<dialog id="img1" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/data_builder.png" style="max-width:90vw;">
</dialog>

### Create Sales Order local Table
1️⃣ In Data Builder, create a new table. Enter Business Name / Technical Name as `Sales Order`.

2️⃣ Add all required columns and assign appropriate data types.

<p>
  <img
    src="{{ site.baseurl }}/images/sales_order_attributes_1.png"
    alt="sales_order_attributes_1"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img2').showModal()"
  >
</p>

<dialog id="img2" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/sales_order_attributes_1.png" style="max-width:90vw;">
</dialog>

<p>
  <img
    src="{{ site.baseurl }}/images/sales_order_attributes_2.png"
    alt="sales_order_attributes_2"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img3').showModal()"
  >
</p>

<dialog id="img3" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/sales_order_attributes_2.png" style="max-width:90vw;">
</dialog>

3️⃣ Mark `DOCUMENT_ID`, `DOCUMENT_ID_POSITION` as **Key Attributes**. 

4️⃣ Click Save and confirm the business/technical name. Then click Deploy to activate the table.

---

### Create Customer local table
1️⃣ In Data Builder, create a new table. Enter Business Name / Technical Name as `Customer`.

2️⃣ Add required columns and define data types.

<p>
  <img
    src="{{ site.baseurl }}/images/customer_attributes.png"
    alt="customer_attributes"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img4').showModal()"
  >
</p>

<dialog id="img4" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_attributes.png" style="max-width:90vw;">
</dialog>

3️⃣ Mark `CUSTOMER_NUMBER` as the **Key Attribute**.

4️⃣ Click Save and confirm the business/technical name. Then click Deploy to activate the table.

---

### Create Material local table
1️⃣ In Data Builder, create a new table. Enter Business Name / Technical Name as `Material`.

2️⃣ Add required columns and define data types.

<p>
  <img
    src="{{ site.baseurl }}/images/material_attributes.png"
    alt="material_attributes"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img5').showModal()"
  >
</p>

<dialog id="img5" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/material_attributes.png" style="max-width:90vw;">
</dialog>

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

<p>
  <img
    src="{{ site.baseurl }}/images/distr_attributes.png"
    alt="Distr"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img6').showModal()"
  >
</p>

<dialog id="img6" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/distr_attributes.png" style="max-width:90vw;">
</dialog>

3️⃣ Set `DISTRIBUTION_CHANNEL` as the **Key Attribute**

## Data Ingestion

{: .note }
Download the required CSV files from the IBM Box folder:
[IBM Lab - “custom” Data Products, Modeling and SAC reporting](https://ibm.ent.box.com/folder/369590392350?s=n5xb24fwnpfk4x0izfeyxyk4b6leuc2t&tc=collab-folder-invite-treatment-b)

### Import csv files into the local tables 

<p>
  <img
    src="{{ site.baseurl }}/images/upload_icon.png"
    alt="Toolbar"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img7').showModal()"
  >
</p>

<dialog id="img7" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/upload_icon.png" style="max-width:90vw;">
</dialog>

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
<p>
  <img
    src="{{ site.baseurl }}/images/Save_Deploy.png"
    alt="Save_Deploy"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img30').showModal()"
  >
</p>

<dialog id="img30" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Save_Deploy.png" style="max-width:90vw;">
</dialog>
