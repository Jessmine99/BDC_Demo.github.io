---
title: 4.Add Business Semantics
layout: default
nav_order: 5
---

# Add Business Semantics

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

<dialog id="img10" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/Material_dim_2.png" style="max-width:90vw;">
</dialog>

  <p>
  <img
    src="{{ site.baseurl }}/images/Material_dim_3.png"
    alt="Material_dim_3"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img11').showModal()"
  >
</p>

<dialog id="img11" onclick="if(event.target===this)this.close()">
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
    onclick="document.getElementById('img12').showModal()"
  >
</p>

<dialog id="img12" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/distr_dim.png" style="max-width:90vw;">
</dialog>
---

### Create SFDC Dimension View

{: .warning }
*Originally, we would have consumed the data product after publishing it, which would have created the remote table automatically in Datasphere. Since consumption is not possible within the workshop environment, we manually create a table in Datasphere to replicate the same structure and workflow*

### Create SFDC Table
- In `Data Builder`, create a new table  
- Enter Business Name / Technical Name as `SFDC`  
- Add required columns and define data types  
- Mark `Id` as key attribute  
- Click Save and confirm the business/technical name  
- Click Deploy to activate the table  
- Upload `EU_Accounts.csv` file. [#Follow data ingestion steps](#import-csv-files-into-the-local-tables)

### Create SFDC View
- Follow steps [#Follow data modeling steps](#create-material-dimension-view) using the `SFDC` table  
- Rename dimension Business/Technical Name to `SFDC_DIM`  

---

### Create Customer Dimension View

1️⃣ Go to `Data Builder` → `Graphical View` and drag the Customer table from the repository onto the canvas, hovering it onto `Output View 1`.

2️⃣ Click `Output View 1` and in the `Properties Panel` rename the Business Name to `Customer DIM`. Change Semantic Usage to `Dimension` and set Expose for Consumption to `ON`.

3️⃣ In the `Properties Panel`, click `Edit Attributes` and configure:
   - Set `CUSTOMER_NAME` to Semantic Type `Text`.
   - Set `LATITUDE` and `LONGITUDE` to Semantic Type `Latitude` and `Longitude`.
   - Set `Text/Association` column `CUSTOMER_NUMBER` → `CUSTOMER_NAME`.

4️⃣ Select the `Customer DIM` node and choose the `Calculated Columns operator` from the popup menu. Click the "+" icon to add a new column, choose `Geo-Coordinates Column`, rename it to `CustomerLocation`, and verify `LATITUDE` and `LONGITUDE` are correctly assigned.

5️⃣ Add a hierarchy by selecting the Customer DIM view, clicking the `Hierarchy icon` (top right in Properties), choosing Level-Based Hierarchy, renaming it to `LocationHierarchy`, and adding levels `COUNTRY_NAME` and `CITY`.

6️⃣ Drag the `Distribution Channel DIM` onto the canvas and hover it onto the calculated "fx" operator until Join appears, then select Join. In the Properties Panel choose Left Join and ensure `DISTRIBUTION_CHANNEL` columns are correctly mapped.

7️⃣ Click the `Projection operator` next to the Left Join. Exclude the `DISTRIBUTION_CHANNEL` column that is set as a key using the (...) menu. If the **non-key** `DISTRIBUTION_CHANNEL` column is excluded, click Restore so that **only one** business key remains.

8️⃣ Drag `SFDC_DIM` onto the canvas → Hover the dimension over the `Customer_DIM` node until the option **Join** or **Union** appears → Select **Join**.

   In the Properties Panel, choose **Left Join**.  
   Ensure the columns `ERP_Customer_Code` and `Customer Number` are linked/mapped.

   `Customer_DIM` will now contain **two duplicated columns** due to the join.  
   Click the **Projection** operator (next to the Left Join operator).

   Exclude the `ERP_Customer_Code` column (click `...` next to the attribute).  
   Also exclude the `Id` column 
   
   {: .important }
   A dimension should have **one business key**.

9️⃣ Click **Save and Deploy** the view.

🔟 Select the **Output Node**, open **Data Viewer** to preview the data.  
   Then go to **Data Persistence** in the Properties Panel and click **Start Data Persistence**.

---

### Create Sales Order Fact Table

1️⃣ Go to `Data Builder` → `New Graphical View` and drag the `Sales Order table` from the repository onto the canvas, hovering it onto Output View 1.

2️⃣ Click `Output View 1` and in the Properties Panel rename the Business Name to `Sales Order Fact`. Change Semantic Usage to `Fact` and set Expose for Consumption to `ON`.

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

5️⃣ In the `Properties Panel`, scroll to the `Associations` section and click the “+” button to create a new Association.
   - Select `Material DIM` as the association target and map `MATERIAL` → `MATERIAL_ID`.
   - Repeat for `Customer DIM` and map `SOLD_TO_CUSTOMER` → `CUSTOMER_NUMBER`.
   - Repeat for `Time Dimension - Day` and map `ORDER_DATE_KEY` → `Date`.
 
 {: .note }
 Choose the technical name not the business name with the link as it will open a new page.

6️⃣ Click Save and Deploy the view.

7️⃣ Select the output node, open `Data Viewer` to preview the data, then go to `Data Persistence` in the `Properties Panel` and click `Start Data Persistence`.

8️⃣ Go to the toolbar → `Tools` → `Impact and Lineage Analysis` icon. Switch from `Data Analysis` to `Dependency Analysis` to view all related objects and associations of the `Sales Order Fact` within the user space.
