# BDC_Demo.github.io
E2E sales analytics demo using SAP Datasphere, SAP Analytics Cloud and SAP Databricks. Build and model data, create an analytic model and vizualize insights using interactive charts, tables and geo maps for actionable business insights.

## Log on to Datasphere
Use credentials that are already given to you

## Explore your own space
### Create time dimensions & tables
Navigate to space managemenent. Select the edit button on your assigned space, where your username is displayed. Scroll down in the time section where you can generate time data for your space. Click edit on time data. When you update the year range, this will generate time tables with data and dimension views.

### Preview time dimensions & tables
Select Repository Explorer in the side navigation area. You should see:
4 views of type Dimension
3 local tables of type Text
1 local table of type Relational Dataset

## Data acquisition
Open Data Builder on your space. Navigate to Data Builder and select your space.

### Create Sales Order local Table
1️⃣ In Data Builder, create a new table. Enter Business Name / Technical Name as `Sales Order`.

2️⃣ Add all required columns and assign appropriate data types.

3️⃣ Mark `DOCUMENT_ID`, `DOCUMENT_ID_POSITION` as **Key Attributes**. 

4️⃣ Click Save and confirm the business/technical name. Then click Deploy to activate the table.

---

### Create Customer local table
1️⃣ In Data Builder, create a new table. Enter Business Name / Technical Name as `Customer`.

2️⃣ Add required columns and define data types.

3️⃣ Mark `CUSTOMER_NUMBER` as the **Key Attribute**.

4️⃣ Click Save and confirm the business/technical name. Then click Deploy to activate the table.

---

### Create Material local table
1️⃣ In Data Builder, create a new table. Enter Business Name / Technical Name as `Material`.

2️⃣ Add required columns and define data types.

3️⃣  Mark `MATERIAL_ID` as the **Key Attribute**.

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

3️⃣ Set `DISTRIBUTION_CHANNEL` as the **Key Attribute**

4️⃣ Click save and then click deploy.

## Data Ingestion
### Import csv files into the local tables 
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

## Data Modeling
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

#### 4️⃣ Preview, Save, Deploy and Persist Data
   
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

## Analytic Modeling
### Create Sales Order Analytic Model

1️⃣ Go to `Data Builder` → `New Analytic Model` and drag `Sales Order Fact` onto the canvas.

2️⃣ In the pop-up window, keep all measures, attributes, and associated dimensions selected and click `Add`.

3️⃣ In the `Properties Panel`, enter `Sales Order Analytic Model` as the Analytic Model name.

### Add Projection

4️⃣ Click the `Sales Order Fact` node and in the `Properties Panel` **unselect**:
   - `DOCUMENT_ID`
   - `DOCUMENT_ID_POSITION`
   - `SHIP_TO_CUSTOMER`
   - `TRADE_DESCRIPTION`

5️⃣ Click the `Material DIM` node and **unselect**:
   - `BASE_UOM_CODE`
   - `MAXIMUM_PACKAGE_SIZE`

6️⃣ Click the `Customer DIM` node and **unselect**:
   - `LATITUDE`
   - `LONGITUDE`
   - `CUSTOMER_EFFECTIVE_DATE`
   - `CUSTOMER_CREATED_DATE`

### Create Calculated Measures

7️⃣ Click the `Fact Sources` node → `Measures` → `+` → `Calculated Measure`.

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

1️⃣1️⃣ Create another `Restricted Measure`:

   - Business Name: `Invoice_gross_revenue`
   - Source Measure: `ORDER_AMOUNT_EURO`
   - Expression: `STATUS` = `'7'`
   - Click `Validate`.

### Define Count Distinct Measure

1️⃣2️⃣ In Measures → `+` → `Count Distinct Measure`:
   - Business Name: `Customer Count`
   - Dimension: `SOLD_TO_CUSTOMER`
   - Enable `Is Auxiliary`.

1️⃣3️⃣ Add a `Calculated Measure`:
   - Business Name: `Avg Spend per customer (EUR)`
   - Expression:
     `NET_VALUE_AMOUNT_DOCUMENT_CURRENCY * (ORDER_AMOUNT_EURO / ORDER_AMOUNT_DOCUMENT_CURRENCY) / Customer_Count`
   - Click `Validate`.

*Note: `ORDER_AMOUNT_EURO / ORDER_AMOUNT_DOCUMENT_CURRENCY` represents the exchange rate from document currency to Euro.*

### Define Exception Aggregation Measure

1️⃣4️⃣ Add a `Calculated Measure`:
   - Business Name: `High value products`
   - Expression: `ORDER_AMOUNT_EURO > 900`
   - Click `Validate`.

1️⃣5️⃣ Scroll to `Exception Aggregation` and set:
   - Type: `SUM`
   - Dimension: `MATERIAL (Sales Order Fact)`

### Add Filter Variable

1️⃣6️⃣ In the `Variables` section, add a `Filter Variable`:
   - Dimension: `Year (ORDER_DATE_KEY)`
   - Filter Type: `Interval`
   - From: `2024` To: `2025`

### Save & Preview

1️⃣7️⃣ Click Save and Deploy.

1️⃣8️⃣ Click `Preview` (top right) to validate the analytic model.

## Story
Log in SAP Analytics Cloud. From `product switch` icon (top right corner) next to your username icon choose `SAP Analytics Cloud`

### Import analytic model and create a new story
- Navigation bar --> `Stories` --> `MyStory - Complete` --> Toolbar --> Tools --> `Add new Data` --> `Data from an existing dataset or model` --> From Datasphere list select `SAPDSP` --> Select your datasphere space --> Select the sales order analytic model you created --> Keep the default variables and select `Set` --> Select `Save` from the File menu in the top toolbar --> Ignore the warning and select the `Keep Data source` option  
- Name the story with your username `username_Sales_Analytics_Dashboard`  
- Click `Cancel` on the layouts  

### Edit story and add widgets 
- Open your story in `edit mode` if not already (top right corner)

### Add Gross Sales Numeric Point Chart
- Select the `+ Create a Numeric Point Chart` placeholder in the Header Lane of the template  
- Select `Builder` --> Add measure `ORDER_AMOUNT_EURO`  
- Go back by selecting `Available Objects`  
- Select Add filters `ORDER_DATE_KEY (member)`, select both 2024, 2025  
- Select the Styling paintbrush within the panel --> Scroll down to `Number Format` --> Scale to `Million` and Scale `Format` to `Thousand, Million, Billion` 
- Close the panel  
- Select More Actions (…) on the Numeric Point chart --> More Options -> Show/Hide -> deselect `Primary Value Labels`  
- Update the chart title: Double click on `ORDER_AMOUNT_EURO` and enter `Global Gross Sales`  

### Add Time Series Chart
- Select the `+ Create a Time Series chart` placeholder --> Available objects --> Drag `ORDER_AMOUNT_EURO` to Measures, and `ORDER_DATE_KEY` to `Time location`  
- Click on the `right side panel` icon from the toolbar to view the chart  
- Click on `1M` in the chart  
- Double click on `ORDER_AMOUNT_EURO per ORDER_DATE_KEY` title and enter `Gross Sales per Order Date`  

### Add tables
- Select the `+ Create a Table` placeholder in the Main Lane of the template  
- In the `Builder` tab under `Rows`, select `+ Add Dimension` --> Select `SOLD_TO_CUSTOMER`, `SALES_ORGANIZATION` --> Click outside the Dimension Dropdown to close it  
- Add your column dimensions --> Under `Columns`, select `+ Add Dimension` --> Select `ORDER_DATE_KEY`  
- Change the measure column --> Select `Set Filters for Measures` --> Select `Invoice gross revenue` and `% Discount`  

### Add Geo Maps
- Select the `+ Create a Geo Map` placeholder in the Main Lane of the template  
- In the `Builder` tab under `Content layer`, select `Layer Type` --> `Choropleth/Drill`, `Layer Style` --> `Bubble`, `Location Dimension` --> `Customer Location`
- Close the builder tab and view the map
  
### Input control

### Delete two of the four Input Control placeholders
- Right click on the placeholders and then select `Delete`  

### Create a Date Input Control (filter)
- Select the `+ Create an Input Control` placeholder in the Filter Lane of the template --> Dimensions --> `ORDER_DATE_KEY` --> filter by member --> Select all years --> Click `OK`  
- Select the widget, when you see a blue box around the widget, resize it down  

### Create a Sales Organization Input Control (filter)
- Select the `+ Create an Input Control` placeholder in the Filter Lane of the template --> Dimensions --> `SALES_ORGANIZATION` --> filter by member --> Select all --> Click `OK`  
- Select the widget, when you see a blue box around the widget, resize it down  

### Linked Analysis
- Right click on `ORDER_DATE_KEY` input control --> select `Linked Analysis` -> `Settings` --> `Only selected widgets` --> Click on the select widgets icon (overlapping squares) --> Tick all boxes except for the last one (`Global Gross Sales`) --> Click `OK` --> Select `Apply`  
- Repeat the Linked Analysis steps for the `SALES_ORGANIZATION` input control  
- Save your story  

### Navigate the input control
- Deselect 2024, then select `Apply Selections` and see changes in Time Series chart  
- Deselect 3975 sales org, then select `Apply Selections` and see changes in the table  
- You will notice that all the widgets are updated, except for the `Global Gross Sales` KPI  

### Just Ask
- Launch Just Ask: Click on the light bulb icon from the toolbar (top right)  
- Select the dropdown list to the left of the search field --> `Add Another Model to Search` --> `SAPDSP` --> select your SAP Datasphere space --> select `sales order analytic model` --> keep default values and select `Set`  

### Using Suggestions
- In the query input field, type `show me avg order price`  
- You can type other dimensions, measures or related objects you want to see  

### Selecting Measure and Dimension
- By selecting the `+ Add to Search` icon at the left of the search bar, you can directly select from the list of available measures and dimensions of the data model, to populate the search field  

### Search for Data
- In the query input field, `show invoice_gross_revenue by region`  
- By default results are displayed as a chart  
- Update the search by entering `show invoice_gross_revenue by region, country in 2024 as pie chart`  
- Select the `Edit Chart` option  
- In the right panel, the chart type and the measure can be replaced or further dimensions added  

### Data Analyzer
- Click on `Data Analyzer` (in the navigation area) → Select `From an Existing Model` → Follow the same steps as before and choose the `Sales Order Analytic Model`  
- Explore the available dimensions and attributes to analyze the data  

*The tool is similar to the Analytic Model Preview tool of SAP Datasphere in terms of functionality and handling*

## SAP Databricks
Log in SAP Databricks. From `product switch` icon (top right corner) next to your username icon choose `SAP Databricks`

## Data Ingestion (Bronze Layer - Raw Data)
- Click on `+New` at the top left --> `Add or upload data` --> Choose `EU_Accounts` csv file.  
- In the catalog, choose `hana_cloud_dbx_catalog` and for the schema choose `bronze`  
- Click on `Create Table`  

---

## Data Modeling (Silver - Gold Layer)
- Workspace --> Users --> Click on your username --> Click on the 3 vertical dots next to `Share` on top right corner --> `Import` --> `EU_Accounts (Data Modeling)` notebook  
- Open the notebook and run the code  
- A refined table with key attributes and defined data types is created  

## Delta Sharing
- Catalog --> `hana_cloud_dbx_catalog` --> `gold` schema --> `eu_accounts`  
- Select `Share` on the top right corner --> `Share via Delta Sharing` --> Create a new share with a view  
- Share name: `EU_Accounts_(your Username)` --> Recipient: `Business Data Cloud` 

## Publish Data Product
- Workspace --> Users --> Click on your username --> Click on the 3 vertical dots next to `Share` on top right corner --> `Import` --> Import `Publish_Data_Product_EU_Accounts` notebook   
- Open the notebook. From navigation bar on the right --> choose environment `V3`  
- In code block: `share_name = "eu_accounts_yourusername"` **(ensure your username is lowercase)**  
- Run all code blocks  

### Verify Data Product is Published
- Log in to SAP Datasphere  
- Go to `Catalog & Marketplace` and in the search bar type your `share_name`  

*It might take a few minutes for the data product to appear*  

## Install Data Product
Not possible due to restrictions associated with the academy account.  

## Data Acquisition/Ingestion

*Originally, we would have consumed the data product after publishing it, which would have created the remote table automatically in Datasphere. Since consumption is not possible, we manually create a table in Datasphere to replicate the same structure and workflow*

### Create SFDC Table
- In `Data Builder`, create a new table  
- Enter Business Name / Technical Name as `SFDC`  
- Add required columns and define data types  
- Mark `Id` as key attribute  
- Click Save and confirm the business/technical name  
- Click Deploy to activate the table  
- Upload `EU_Accounts.csv` file. [#Follow data ingestion steps](#import-csv-files-into-the-local-tables)

## Data Modeling
### Create SFDC View
- Follow steps [#Follow data modeling steps](#create-material-dimension-view) using the `SFDC` table  
- Rename dimension Business/Technical Name to `SFDC_DIM`  

### Join SFDC_DIM with Customer DIM
- Open `Customer_DIM`  
- Drag `SFDC_DIM` on the canvas --> Hover the dimension onto `Customer_DIM` node until the option `Join` or `Union` appears --> Choose `Join`  
- Choose `Left Join` in the properties  
- Ensure columns `ERP_Customer_Code` and `Customer Number` are linked/mapped  

### Exclude Columns
- `Customer_DIM` now has 2 duplicated columns due to the join  
- Click on the `Projection` operator (next to the Left Join operator)  
- Exclude the `ERP_Customer_Code` column (click `...` next to the attribute)  
- Also exclude `Id` column (a dimension should have ONE business key)  

### Preview, Save & Deploy, and Persist Data
- [#Follow Preview, Save & Deploy, and Persist Data](#create-material-dimension-view)

## Update Analytic Model
- Open `Sales Order Analytic Model` and redeploy  
- Click on `sold_to_customer` node and from the properties panel **include** columns: `qualityscore`, `accounttype`, `industry`, `inactive` by ticking the box  
- Save and deploy model  

## Enhance SAC Story
- Log in to SAC   
- Open your story in `edit mode`  
- Toolbar --> `View` --> `left side panel` --> `Outline` --> `Add second page`  
- Go to `page 2` and click on `Assets`  

### Column Chart: Revenue by Account Type & Industry
- From `widgets`, drag `Chart` in the storyboard page 2  
- Choose data source and the analytic model you created  
- From `Builder panel` --> Chart orientation: `Vertical`  
- Measures: `ORDER_AMOUNT_EURO`  
- Dimensions: `Industry`  
- Color: `accounttype`  
- Double click on the chart title and change it to: `Revenue per account type & industry`  

### Heatmap: High Value Products per Account Type & QualityScore
- From `widgets`, drag `Chart` in the storyboard  
- Choose data source and the analytic model you created  
- From Builder panel --> Selected chart: `Heatmap`  
- Color: `High value products`  
- Dimensions: `qualityscore` (X-axis), `accounttype` (Y-axis)  
- Change title to: `Number of high value products per accounttype, qualityscore`  

#### Interpretation
- Color intensity → Magnitude  
  - Darker / Blue = higher value  
  - Lighter / Pink = lower value  

**Examples:**  
- Monitoring – Quality Score 7 → 333 → Monitoring customers with quality score 7 generate many high-value products  
- Strategic – Quality Score 5 → 251 → Strategic customers with medium quality score generate strong high-value output  
- Target – Quality Score 1 → 336 → Low-quality Target accounts produce high-value products → growth opportunity or risk  


