---
title: 5.Data Modeling for Salesforce data
layout: default
nav_order: 6
---

# Add Business Semantics to Salesforce data

### Create SFDC Dimension View

{: .warning }
*Originally, we would have consumed the data product after publishing it, which would have created the remote table automatically in Datasphere. Since consumption is not possible within the workshop environment, we manually create a table in Datasphere to replicate the same structure and workflow*

### Create SFDC Table
- In `Data Builder`, create a new table  
- Enter Business Name / Technical Name as `SFDC`  
- Add required columns and define data types 
  <p>
  <img
    src="{{ site.baseurl }}/images/SFDC_attributes.png"
    alt="SFDC_attributes"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img16').showModal()"
  >
</p>

<dialog id="img16" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/SFDC_attributes.png" style="max-width:90vw;">
</dialog> 
- Mark `Id` as key attribute  
- Click Save and confirm the business/technical name  
- Click Deploy to activate the table  
- Upload `account_clusters.csv` file. [Follow data ingestion steps](#Import-csv-files-into-the-local-tables)

### Create SFDC View
- [Follow data modeling steps](#create-material-dimension-view) using the `SFDC` table  
- Rename dimension Business/Technical Name to `SFDC_DIM`  
 <p>
  <img
    src="{{ site.baseurl }}/images/SFDC_Dim.png"
    alt="SFDC_Dim"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img17').showModal()"
  >
</p>

<dialog id="img17" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/SFDC_Dim.png" style="max-width:90vw;">
</dialog> 
---

### Enrich Customer Dimension View

Go to `Data Builder` --> `Customer DIM`

Drag `SFDC_DIM` onto the canvas → Hover the dimension over the `Customer_DIM` node until the option **Join** or **Union** appears → Select **Join**.

   In the Properties Panel, choose **Left Join**.  
   Ensure the columns `ERP_Customer_Code` and `Customer Number` are linked/mapped.
   <p>
  <img
    src="{{ site.baseurl }}/images/customer_dim_join_2.png"
    alt="customer_dim_join_2"
    style="width:300px; cursor:pointer;"
    onclick="document.getElementById('img25').showModal()"
  >
</p>

<dialog id="img25" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_dim_join_2.png" style="max-width:90vw;">
</dialog> 
   `Customer_DIM` will now contain **two duplicated columns** due to the join.  
   Click the `Projection operator` next to the Left Join.

   Exclude the `ERP_Customer_Code` column (click `...` next to the attribute).  
   Also exclude the `Id` column 
   
   {: .important }
   A dimension should have **one business key**.

<p>
  <img
    src="{{ site.baseurl }}/images/customer_dim_canvas_2.png"
    alt="customer_dim_customer_dim_canvas_2"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img31').showModal()"
  >
</p>

<dialog id="img31" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/customer_dim_canvas_2.png" style="max-width:90vw;">
</dialog>
9️⃣ Click **Save and Deploy** the view.

🔟 Select the **Output Node**, open **Data Viewer** to preview the data.  
   Then go to **Data Persistence** in the Properties Panel and click **Start Data Persistence**.

---
