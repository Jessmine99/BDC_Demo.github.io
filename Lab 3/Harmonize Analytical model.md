---
title: 6.Harmonize Analytical model
layout: default
nav_order: 7
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

### Add Projection
4️⃣ Click the `Sales Order Fact` node and in the `Properties Panel` **unselect**:
   - `DOCUMENT_ID`
   - `DOCUMENT_ID_POSITION`
   - `SHIP_TO_CUSTOMER`
   - `TRADE_DESCRIPTION`
 <p>
  <img
    src="{{ site.baseurl }}/images/Sales_Order_Fact_Node.png"
    alt="Sales_Order_Fact_Node"
    style="width:300px; cursor:pointer;"
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
    style="width:300px; cursor:pointer;"
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
   - `Id`
   - `ERP_Customer_Code`
<p>
  <img
    src="{{ site.baseurl }}/images/Customer_Dim_Node.png"
    alt="Customer_Dim_Node"
    style="width:300px; cursor:pointer;"
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
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img36').showModal()"
  >
</p>

<dialog id="img36" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Fact_Sources_Node.png" style="max-width:90vw;">
</dialog>
8️⃣ Create:
   - Business Name: `Avg Order Price`
   - Expression: `ORDER_AMOUNT_EURO / QUANTITY`
   - Click `Validate`.

9️⃣ Repeat to create:
   - Business Name: `% Discount`
   - Expression: `DISCOUNT_AMOUNT_DOCUMENT_CURRENCY` / `ORDER_AMOUNT_DOCUMENT_CURRENCY`
   - Click `Validate`.

### Add Restricted Measures

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
1️⃣1️⃣ Create another `Restricted Measure`:

   - Business Name: `Invoice_gross_revenue`
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

1️⃣2️⃣ In Measures → `+` → `Count Distinct Measure`:
   - Business Name: `Customer Count`
   - Dimension: `SOLD_TO_CUSTOMER`
   - Enable `Is Auxiliary`.
<p>
  <img
    src="{{ site.baseurl }}/images/Customer_count.png"
    alt="Customer_count"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img39').showModal()"
  >
</p>

<dialog id="img39" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Customer_count.png" style="max-width:90vw;">
</dialog>

1️⃣3️⃣ Add a `Calculated Measure`:
   - Business Name: `Avg Spend per customer (EUR)`
   - Expression:
     `NET_VALUE_AMOUNT_DOCUMENT_CURRENCY * (ORDER_AMOUNT_EURO / ORDER_AMOUNT_DOCUMENT_CURRENCY) / Customer_Count`
   - Click `Validate`.

*Note: `ORDER_AMOUNT_EURO / ORDER_AMOUNT_DOCUMENT_CURRENCY` represents the exchange rate from document currency to Euro.*
<p>
  <img
    src="{{ site.baseurl }}/images/Avg_spend_per_cust.png"
    alt="Avg_spend_per_cust"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img40').showModal()"
  >
</p>

<dialog id="img40" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Avg_spend_per_cust.png" style="max-width:90vw;">
</dialog>

### Define Exception Aggregation Measure
1️⃣4️⃣ Add a `Calculated Measure`:
   - Business Name: `Expensive products`
   - Expression: `CASE WHEN (ORDER_AMOUNT_EURO / QUANTITY) > 900 THEN 1 ELSE 0 END`
   - Click `Validate`.

 Scroll to `Exception Aggregation` and set:
   - Type: `SUM`
   - Dimension: `MATERIAL (Sales Order Fact)`

### Add Filter Variable
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