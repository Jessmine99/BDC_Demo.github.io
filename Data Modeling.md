---
title: Data Modeling
layout: default
nav_order: 3
---

# Data Modeling

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

3️⃣ Define Semantic Types & Text Associations

 In the Properties Panel, click `Edit Attributes` and configure:

- Set Semantic Type to `Text`:
  - `MATERIAL_DESCRIPTION`
  - `MATERIAL_TYPE_DESCRIPTION`

- Set Text/Association Columns:
  - `MATERIAL_ID` → `MATERIAL_DESCRIPTION`
  - `MATERIAL_TYPE_CODE` → `MATERIAL_TYPE_DESCRIPTION`

4️⃣ Preview, Save, Deploy and Persist Data
   
 - Click save and then deploy
 - Select the Material Dimension output node, Choose  `Data Viewer ` to preview data
 - In the Properties Panel → Go to Data Persistence. Click Start  `Data Persistence `

---

### Create Distribution Channel Dimension

Repeat the same steps as above using the `DIST_CHANNEL` table and rename dimension business/technical name to `Distribution Channel DIM`

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

8️⃣ Click Save and Deploy the view.

9️⃣ Select the output node, open `Data Viewer` to preview the data, then go to `Data Persistence` in the Properties Panel and click `Start Data Persistence`.

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
 
 *Choose the technical name not the business name with the link as it will open a new page.*

6️⃣ Click Save and Deploy the view.

7️⃣ Select the output node, open `Data Viewer` to preview the data, then go to `Data Persistence` in the `Properties Panel` and click `Start Data Persistence`.

8️⃣ Go to the toolbar → `Tools` → `Impact and Lineage Analysis` icon. Switch from `Data Analysis` to `Dependency Analysis` to view all related objects and associations of the `Sales Order Fact` within the user space.
