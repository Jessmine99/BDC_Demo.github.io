---
title: 7.SAC Story
layout: default
nav_order: 2
parent: Lab 3
---

# SAC Story

Log in SAP Analytics Cloud. From `product switch` icon (top right corner) next to your username icon choose `SAP Analytics Cloud`

<p>
  <img
    src="{{ site.baseurl }}/images/log in.png"
    alt="log in"
    style="width:400px; cursor:pointer;"
    onclick="document.getElementById('img44').showModal()"
  >
</p>

<dialog id="img44" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/log in.png" style="max-width:90vw;">
</dialog>

### Import analytic model and create a new story
- Navigation bar --> `Stories` --> `MyStory - Complete` --> Toolbar --> Tools --> `Add new Data` --> `Data from an existing dataset or model` --> From Datasphere list select `SAPDSP` --> Select your datasphere space --> Select the sales order analytic model you created --> Keep the default variables and select `Set` --> Select `Save` from the File menu in the top toolbar --> Ignore the warning and select the `Keep Data source` option  
- Name the story with your username `username_Sales_Analytics_Dashboard`  
- Click `Cancel` on the layouts  

### Edit story and add widgets 
- Open your story in `edit mode` if not already (top right corner)

### Add Gross Sales Numeric Point Chart

**To provide a quick overview of sales performance, we create a KPI that shows the total global gross sales for the selected time period.**

- Select the `+ Create a Numeric Point Chart` placeholder in the Header Lane of the template  
- Select `Builder` --> Add measure `ORDER_AMOUNT_EURO`  
- Go back by selecting `Available Objects`  
- Select Add filters `ORDER_DATE_KEY (member)`, select both 2024, 2025  
- Select the Styling paintbrush within the panel --> Scroll down to `Number Format` --> Scale to `Million` and Scale `Format` to `Thousand, Million, Billion` 
- Close the panel  
- Select More Actions (…) on the Numeric Point chart --> More Options -> Show/Hide -> deselect `Primary Value Labels`  
- Update the chart title: Double click on `ORDER_AMOUNT_EURO` and enter `Global Gross Sales` 

### Add Time Series Chart

**To understand how sales evolve over time, we create a chart that shows gross sales by order date.**

- Select the `+ Create a Time Series chart` placeholder --> Available objects --> Drag `ORDER_AMOUNT_EURO` to Measures, and `ORDER_DATE_KEY` to `Time location`  
- Click on the `right side panel` icon from the toolbar to view the chart  
- Click on `1M` in the chart  
- Double click on `ORDER_AMOUNT_EURO per ORDER_DATE_KEY` title and enter `Gross Sales per Order Date`  

**To explore the data in more detail, we create a table that shows sales performance by customer and sales organization, including revenue and discounts.**
### Add tables
- Select the `+ Create a Table` placeholder in the Main Lane of the template  
- In the `Builder` tab under `Rows`, select `+ Add Dimension` --> Select `SOLD_TO_CUSTOMER`, `SALES_ORGANIZATION` --> Click outside the Dimension Dropdown to close it  
- Add your column dimensions --> Under `Columns`, select `+ Add Dimension` --> Select `ORDER_DATE_KEY`  
- Change the measure column --> Select `Set Filters for Measures` --> Select `Invoice gross revenue` and `% Discount`  

### Add Geo Maps

**To understand the geographic distribution of sales, we create a map that shows customer locations and sales activity across regions.**

- Select the `+ Create a Geo Map` placeholder in the Main Lane of the template  
- In the `Builder` tab under `Content layer`, select `Layer Type` --> `Choropleth/Drill`, `Layer Style` --> `Bubble`, `Location Dimension` --> `Customer Location`
- Close the builder tab and view the map
  
### Input control

**To make the dashboard interactive, we add input controls that allow users to filter the data by year and sales organization**

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

### Create page 2 
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

{: .note }
The tool is similar to the Analytic Model Preview tool of SAP Datasphere in terms of functionality and handling
