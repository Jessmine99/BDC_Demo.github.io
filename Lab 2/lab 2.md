---
title: Lab 2
layout: default
nav_order: 3
has_children: true
---
# Lab 2
In this section, we enrich the sales analysis with additional customer insights from Salesforce.

Customer account data is first loaded into SAP Databricks, where it is prepared and structured through a data pipeline. The data is cleaned, organized, and transformed into a dataset that is ready for analysis.

Next, a machine learning clustering model groups customers with similar characteristics, helping identify different customer segments.

The resulting dataset is then shared back to SAP Datasphere and integrated into the existing customer data model. This allows the sales analytics solution to analyze sales performance together with customer segments, industries, and account types.

<p>
  <img
    src="{{ site.baseurl }}/images/lab 2.png"
    alt="lab 2"
    style="width:800px; cursor:pointer;"
    onclick="document.getElementById('img45').showModal()"
  >
</p>

<dialog id="img45" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/lab 2.png" style="max-width:90vw;">
</dialog>