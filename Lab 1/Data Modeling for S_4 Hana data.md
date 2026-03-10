---
title: 2.Data Modeling for S/4 HANA data
layout: default
nav_order: 3
---

# Add Business Semantics to S/4 HANA data

### Create Material Dimension View

1️⃣ Create Graphical View
    Go to Data Builder → Graphical View. Drag the `Material` table from the repository onto the canvas. Hover it onto Output View 1.
    The output node represents the final dataset and properties of the model.

2️⃣ Set Semantics
    Click Output View 1.
    
 - In the Properties Panel:   
    - Rename Business Name to `Material DIM`  
    - Change Semantic Usage to `Dimension`
    - Set Expose for Consumption to `ON`
<p>
  <img
    src="{{ site.baseurl }}/images/Material_dim_1.png"
    alt="Material_dim_1"
    style="width:400px; cursor:pointer;"
    onclick="document.getElementById('img10').showModal()"
  >
</p>

<dialog id="img10" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Material_dim_1.png" style="max-width:90vw;">
</dialog>

3️⃣ Define Semantic Types & Text Associations

 In the Properties Panel, click `Edit Attributes` and configure:

- Set Semantic Type to `Text`:
  - `MATERIAL_DESCRIPTION`
  - `MATERIAL_TYPE_DESCRIPTION`

- Set Text/Association Columns:
  - `MATERIAL_ID` → `MATERIAL_DESCRIPTION`
  - `MATERIAL_TYPE_CODE` → `MATERIAL_TYPE_DESCRIPTION`

  <p>
  <img
    src="{{ site.baseurl }}/images/Material_dim_2.png"
    alt="Material_dim_2"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img11').showModal()"
  >
</p>

<dialog id="img11" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Material_dim_2.png" style="max-width:90vw;">
</dialog>

  <p>
  <img
    src="{{ site.baseurl }}/images/Material_dim_3.png"
    alt="Material_dim_3"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img12').showModal()"
  >
</p>

<dialog id="img12" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Material_dim_3.png" style="max-width:90vw;">
</dialog>

4️⃣ Preview, Save, Deploy and Persist Data
   
 - Click save and then deploy
 - Select the Material Dimension output node, Choose  `Data Viewer ` to preview data
 - In the Properties Panel → Go to Data Persistence. Click Start  `Data Persistence `

---

### Create Distribution Channel Dimension View

Repeat the same steps as above using the `DIST_CHANNEL` table and rename dimension business/technical name to `Distribution Channel DIM`

  <p>
  <img
    src="{{ site.baseurl }}/images/distr_dim.png"
    alt="distr_dim"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img13').showModal()"
  >
</p>

<dialog id="img13" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/distr_dim.png" style="max-width:90vw;">
</dialog>
---

### Create Customer Dimension View

1️⃣ Go to `Data Builder` → `Graphical View` and drag the Customer table from the repository onto the canvas, hovering it onto `Output View 1`.

2️⃣ Click `Output View 1` and in the `Properties Panel` rename the Business Name to `Customer DIM`. Change Semantic Usage to `Dimension` and set Expose for Consumption to `ON`.
 <p>
  <img
    src="{{ site.baseurl }}/images/customer_dim_properties.png"
    alt="customer_dim_properties"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img18').showModal()"
  >
</p>

<dialog id="img18" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_dim_properties.png" style="max-width:90vw;">
</dialog> 
3️⃣ In the `Properties Panel`, click `Edit Attributes` and configure:
   - Set `CUSTOMER_NAME` to Semantic Type `Text`.
   - Set `LATITUDE` and `LONGITUDE` to Semantic Type `Latitude` and `Longitude`.
   - Set `Text/Association` column `CUSTOMER_NUMBER` → `CUSTOMER_NAME`.
 <p>
  <img
    src="{{ site.baseurl }}/images/customer_dim_model_properties.png"
    alt="customer_dim_model_properties"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img19').showModal()"
  >
</p>

<dialog id="img19" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_dim_model_properties.png" style="max-width:90vw;">
</dialog> 
4️⃣ Select the `Customer DIM` node and choose the `Calculated Columns operator` from the popup menu. Click the "+" icon to add a new column, choose `Geo-Coordinates Column`, rename it to `CustomerLocation`, and verify `LATITUDE` and `LONGITUDE` are correctly assigned.
 <p>
  <img
    src="{{ site.baseurl }}/images/customer_dim_calculated_col.png"
    alt="customer_dim_calculated_col"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img20').showModal()"
  >
</p>

<dialog id="img20" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_dim_calculated_col.png" style="max-width:90vw;">
</dialog>
5️⃣ Add a hierarchy by selecting the Customer DIM view, clicking the `Hierarchy icon` (top right in Properties), choosing Level-Based Hierarchy, renaming it to `LocationHierarchy`, and adding levels `COUNTRY_NAME` and `CITY`.
 <p>
  <img
    src="{{ site.baseurl }}/images/customer_dim_hierarchy.png"
    alt="customer_dim_hierarchy"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img21').showModal()"
  >
</p>

<dialog id="img21" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_dim_hierarchy.png" style="max-width:90vw;">
</dialog>
6️⃣ Drag the `Distribution Channel DIM` onto the canvas and hover it onto the calculated "fx" operator until Join appears, then select Join. In the Properties Panel choose Left Join and ensure `DISTRIBUTION_CHANNEL` columns are correctly mapped.
 <p>
  <img
    src="{{ site.baseurl }}/images/customer_dim_join_1.png"
    alt="ccustomer_dim_customer_dim_join_1"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img22').showModal()"
  >
</p>

<dialog id="img22" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_dim_join_1.png" style="max-width:90vw;">
</dialog>
7️⃣ Click the `Projection operator` next to the Left Join. Exclude the `DISTRIBUTION_CHANNEL` column that is set as a key using the (...) menu. If the **non-key** `DISTRIBUTION_CHANNEL` column is excluded, click Restore so that **only one** business key remains.
<p>
  <img
    src="{{ site.baseurl }}/images/customer_dim_join_1.1.png"
    alt="ccustomer_dim_customer_dim_join_1.1"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img23').showModal()"
  >
</p>

<dialog id="img23" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_dim_join_1.1.png" style="max-width:90vw;">
</dialog>

<p>
  <img
    src="{{ site.baseurl }}/images/customer_dim_canvas_1.png"
    alt="ccustomer_dim_customer_dim_canvas_1"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img24').showModal()"
  >
</p>

<dialog id="img24" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_dim_canvas_1.png" style="max-width:90vw;">
</dialog>

8️⃣Click **Save and Deploy** the view.

9️⃣ Select the **Output Node**, open **Data Viewer** to preview the data.  
   Then go to **Data Persistence** in the Properties Panel and click **Start Data Persistence**.

---

### Create Sales Order Fact Table

1️⃣ Go to `Data Builder` → `New Graphical View` and drag the `Sales Order table` from the repository onto the canvas, hovering it onto Output View 1.
<p>
  <img
    src="{{ site.baseurl }}/images/sales_order_fact_canvas.png"
    alt="sales_order_fact_canvas"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img26').showModal()"
  >
</p>

<dialog id="img26" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/sales_order_fact_canvas.png" style="max-width:90vw;">
</dialog>
2️⃣ Click `Output View 1` and in the Properties Panel rename the Business Name to `Sales Order Fact`. Change Semantic Usage to `Fact` and set Expose for Consumption to `ON`.
<p>
  <img
    src="{{ site.baseurl }}/images/sales_order_fact_properties.png"
    alt="sales_order_fact_properties"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img27').showModal()"
  >
</p>

<dialog id="img27" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/sales_order_fact_properties.png" style="max-width:90vw;">
</dialog>
3️⃣ In the `Properties Panel`, click `Edit Attributes` and configure:
   - Assign Semantic Type `Currency Code` to `SO_CURRENCY_CODE`.
   - Assign Semantic Type `Text` to `STATUS_DESCRIPTION`.
   - Set Text/Association column `STATUS` → `STATUS_DESCRIPTION`.

4️⃣ Select the More (…) menu for the following columns and change them to `Measure`:
   - `DISCOUNT_AMOUNT_DOCUMENT_CURRENCY`
   - `NET_VALUE_AMOUNT_DOCUMENT_CURRENCY`
   - `ORDER_AMOUNT_DOCUMENT_CURRENCY`
   - `ORDER_AMOUNT_EURO`
   - `QUANTITY`
<p>
  <img
    src="{{ site.baseurl }}/images/sales_order_fact_measures.png"
    alt="sales_order_fact_measures"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img28').showModal()"
  >
</p>

<dialog id="img28" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/sales_order_fact_measures.png" style="max-width:90vw;">
</dialog>
5️⃣ In the `Properties Panel`, scroll to the `Associations` section and click the “+” button to create a new Association.

{: .note }
At the assocation target box choose the technical name not the business name with the link as it will open a new page.

   - Select `Material DIM` as the association target and map `MATERIAL` → `MATERIAL_ID`.
   - Repeat for `Customer DIM` and map `SOLD_TO_CUSTOMER` → `CUSTOMER_NUMBER`.
   - Repeat for `Time Dimension - Day` and map `ORDER_DATE_KEY` → `Date`.
 <p>
  <img
    src="{{ site.baseurl }}/images/sales_order_fact_associations.png"
    alt="sales_order_fact_associations"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img29').showModal()"
  >
</p>

<dialog id="img29" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/sales_order_fact_associations.png" style="max-width:90vw;">
</dialog>

6️⃣ Click Save and Deploy the view.

7️⃣ Select the output node, open `Data Viewer` to preview the data, then go to `Data Persistence` in the `Properties Panel` and click `Start Data Persistence`.

8️⃣ Go to the toolbar → `Tools` → `Impact and Lineage Analysis` icon. Switch from `Data Analysis` to `Dependency Analysis` to view all related objects and associations of the `Sales Order Fact` within the user space.
<p>
  <img
    src="{{ site.baseurl }}/images/Dependency_Analysis.png"
    alt="Dependency_Analysis"
    style="width:400px; cursor:pointer;"
    onclick="document.getElementById('img32').showModal()"
  >
</p>

<dialog id="img32" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Dependency_Analysis.png" style="max-width:90vw;">
</dialog>
