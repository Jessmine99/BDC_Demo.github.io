---
title: 6.Define Analytical model
layout: default
nav_order: 1
parent: Lab 3
---

# Analytical Model

### Create Sales Order Analytic Model

1️⃣ Go to `Data Builder` → `New Analytic Model` and drag `Sales Order Fact` onto the canvas.

2️⃣ In the pop-up window, keep all measures, attributes, and associated dimensions selected and click `Add`.

3️⃣ In the `Properties Panel`, enter `Sales Order Analytic Model` as the Analytic Model name.
 <p>
  <img
    src="{{ site.baseurl }}/images/Analytic_model_properties.png"
    alt="Analytic_model_properties"
    style="width:400px; cursor:pointer;"
    onclick="document.getElementById('img32').showModal()"
  >
</p>

<dialog id="img32" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Analytic_model_properties.png" style="max-width:90vw;">
</dialog>

### Add Projections

**Hide columns that are not needed for the SAC dashboard.**

4️⃣ Click the `Sales Order Fact` node and in the `Properties Panel` **unselect**:
   - `DOCUMENT_ID`
   - `DOCUMENT_ID_POSITION`
   - `TRADE_DESCRIPTION`
 <p>
  <img
    src="{{ site.baseurl }}/images/Sales_Order_Fact_Node.png"
    alt="Sales_Order_Fact_Node"
    style="width:500px; cursor:pointer;"
    onclick="document.getElementById('img33').showModal()"
  >
</p>

<dialog id="img33" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Sales_Order_Fact_Node.png" style="max-width:90vw;">
</dialog>
5️⃣ Click the `Material DIM` node and in the `Properties Panel` **unselect**:
   - `BASE_UOM_CODE`
   - `MAXIMUM_PACKAGE_SIZE`
<p>
  <img
    src="{{ site.baseurl }}/images/Material_Dim_Node.png"
    alt="Material_Dim_Node"
    style="width:500px; cursor:pointer;"
    onclick="document.getElementById('img34').showModal()"
  >
</p>

<dialog id="img34" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Material_Dim_Node.png" style="max-width:90vw;">
</dialog>
6️⃣ Click the `Customer DIM` node and in the `Properties Panel` **unselect**:
   - `LATITUDE`
   - `LONGITUDE`
   - `CUSTOMER_EFFECTIVE_DATE`
   - `CUSTOMER_CREATED_DATE`
<p>
  <img
    src="{{ site.baseurl }}/images/Customer_Dim_Node.png"
    alt="Customer_Dim_Node"
    style="width:500px; cursor:pointer;"
    onclick="document.getElementById('img35').showModal()"
  >
</p>

<dialog id="img35" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Customer_Dim_Node.png" style="max-width:90vw;">
</dialog>

### Create Calculated Measures

7️⃣ Click the `Fact Sources` node → `Measures` → `+` → `Calculated Measure`.
<p>
  <img
    src="{{ site.baseurl }}/images/Fact_Sources_Node.png"
    alt="Fact_Sources_Node"
    style="width:500px; cursor:pointer;"
    onclick="document.getElementById('img36').showModal()"
  >
</p>

<dialog id="img36" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Fact_Sources_Node.png" style="max-width:90vw;">
</dialog>

**To better understand product pricing, we create a measure that calculates the price per product unit.**

8️⃣ Create:
   - Business Name: `Price per product unit`
   - Expression: `ORDER_AMOUNT_EURO / QUANTITY`
   - Click `Validate`.

**To analyze pricing incentives, we create a measure that calculates the percentage discount applied to orders.**

9️⃣ Repeat to create:
   - Business Name: `% Discount`
   - Expression: `DISCOUNT_AMOUNT_DOCUMENT_CURRENCY / ORDER_AMOUNT_DOCUMENT_CURRENCY`
   - Click `Validate`.

### Add Restricted Measures
**To analyze regional performance, we create a measure that shows revenue generated from customers in France.**

🔟 In Measures → `+` → `Restricted Measure`, create:

   - Business Name: `France revenue`
   - Source Measure: `NET_VALUE_AMOUNT_DOCUMENT_CURRENCY`
   - Expression: `COUNTRY_NAME_SOLD_ `= `'France'`
   - Click `Validate`.
<p>
  <img
    src="{{ site.baseurl }}/images/France_revenue.png"
    alt="France_revenue"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img37').showModal()"
  >
</p>

<dialog id="img37" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/France_revenue.png" style="max-width:90vw;">
</dialog>

**To focus on completed sales, we create a measure that calculates revenue from invoiced orders.**

1️⃣1️⃣ Create another `Restricted Measure`:
   - Business Name: `Invoiced_gross_revenue`
   - Source Measure: `ORDER_AMOUNT_EURO`
   - Expression: `STATUS` = `'7'`
   - Click `Validate`.
<p>
  <img
    src="{{ site.baseurl }}/images/Invoiced_revenue.png"
    alt="Invoiced_revenue"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img38').showModal()"
  >
</p>

<dialog id="img38" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Invoiced_revenue.png" style="max-width:90vw;">
</dialog>

### Define Count Distinct Measure
**To calculate the average spend per customer, we first create a measure that counts the number of unique customers.**

1️⃣2️⃣ In Measures → `+` → `Count Distinct Measure`:
   - Business Name: `Customer Count`
   - Dimension: `SOLD_TO_CUSTOMER`

**Next, we create a measure that calculates the average spending per customer and converts the values to Euros, so customer spending can be compared across different countries.**

1️⃣3️⃣ Add a `Calculated Measure`:
   - Business Name: `Avg Spend per customer (EUR)`
   - Expression:
     `ORDER_AMOUNT_EURO / Customer_Count`
   - Click `Validate`.

### Define Exception Aggregation Measure
**To identify premium products, we create a measure that highlights products with a high price per unit.**

1️⃣4️⃣ Add a `Calculated Measure`:
   - Business Name: `Premium products`
   - Expression: `CASE WHEN Price_per_product_unit > 900 THEN 1 ELSE 0 END`
   - Click `Validate`.

### Add Filter Variable
**To keep the analysis focused on recent sales activity, we add a filter that restricts the data to 2024 and 2025.**

1️⃣5️⃣ In the `Variables` section, add a `Filter Variable`:
   - Dimension: `Year (ORDER_DATE_KEY)`
   - Filter Type: `Interval`
   - From: `2024` To: `2025`
<p>
  <img
    src="{{ site.baseurl }}/images/Filter_variable.png"
    alt="Filter_variable"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img42').showModal()"
  >
</p>

<dialog id="img42" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Filter_variable.png" style="max-width:90vw;">
</dialog>
### Save & Preview

1️⃣6️⃣ Click Save and Deploy.

1️⃣7️⃣ Click `Preview` (top right) to validate the analytic model.
<p>
  <img
    src="{{ site.baseurl }}/images/preview_model.png"
    alt="preview_model"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img43').showModal()"
  >
</p>

<dialog id="img43" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/preview_model.png" style="max-width:90vw;">
</dialog>

{: .note }
**Modular approach:** If you encounter issues in this section, you can upload the provided analytic model and continue with the following steps. File: Sales_Order_Analytic_Model.json
<a href="https://ibm.ent.box.com/folder/369590392350?s=n5xb24fwnpfk4x0izfeyxyk4b6leuc2t&tc=collab-folder-invite-treatment-b" target="_blank">IBM Lab - “custom” Data Products, Modeling and SAC reporting</a>

---

[SAC Story →](SAC Story.md){: .btn .btn-primary }
