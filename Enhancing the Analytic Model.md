# Integrating Salesforce Data into the Analytic Model

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
