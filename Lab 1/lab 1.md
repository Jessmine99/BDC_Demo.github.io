---
title: Lab 1
layout: default
nav_order: 2
has_children: true
---
# Lab 1
In this section, we prepare sales data so it can be analyzed and used to generate business insights.

First, sales data such as customers, materials, and sales orders is loaded into SAP Datasphere. This data represents typical operational information coming from an ERP system.

Next, we create views on top of the tables to organize the data. Separate views are created for customers, materials, and distribution channels to store descriptive information. The sales order data is used to create a sales table that contains the actual transactions, such as order amounts, quantities, and discounts.

These datasets are then connected so that each sales order can be linked to the correct customer, material, and date. This creates a complete view of the sales process that can be easily explored and analyzed.

After the data is prepared and activated, it is ready to be used for analytics. The dataset can then be shared as a data product, allowing other platforms such as SAP Databricks to access it for advanced analytics and machine learning.

<p>
  <img
    src="{{ site.baseurl }}/images/lab 1.png"
    alt="lab 1"
    style="width:800px; cursor:pointer;"
    onclick="document.getElementById('img44').showModal()"
  >
</p>

<dialog id="img44" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/lab 1.png" style="max-width:90vw;">
</dialog>