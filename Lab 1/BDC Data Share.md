---
title: 3.BDC Data Share
layout: default
nav_order: 4
---

# Sharing SAP Business Data Cloud Data Products to SAP Databricks

{: .warning }
This section cannot be performed within the workshop environment.
The steps below are provided for informational purposes to explain the process.

1️⃣ In the side navigation area, go to ‘Data Sharing Cockpit’ → ‘My Data Products’.

<p>
  <img
    src="{{ site.baseurl }}/images/custom_data_product_1.png"
    alt="Data Product 1"
    style="width:180px; cursor:pointer;"
    onclick="document.getElementById('img1').showModal()"
  >
</p>

<dialog id="img1" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/custom_data_product_1.png" style="max-width:90vw;">
</dialog>

2️⃣ Search for ‘Sales Order Fact’, add a description, and select ‘Save Changes’.
<p>
  <img
    src="{{ site.baseurl }}/images/custom_data_product_2.png"
    alt="Data Product 2"
    style="width:400px; cursor:pointer;"
    onclick="document.getElementById('img2').showModal()"
  >
</p>

<dialog id="img2" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/custom_data_product_2.png" style="max-width:90vw;">
</dialog>

3️⃣ Go to ‘Catalog & Marketplace’ from the navigation bar.

4️⃣ Select ‘Marketplace Data Products’, search for your data product, and open it.

5️⃣ In the ‘Details’ section, review the APIs and select ‘Share’ to share the SAP Data Product with ‘SAP Databricks Unity Catalog’.

6️⃣ In ‘Manage Share Access’, enter the name of the ‘Delta Share’ that appears in the target system.  
Leave ‘Workspace’ as the default workspace and select ‘Share’.

7️⃣ The data product is now shared with ‘SAP Databricks’.
