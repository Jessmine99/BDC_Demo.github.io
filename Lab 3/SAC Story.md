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

<p>
  <img
    src="{{ site.baseurl }}/images/KPI.png"
    alt="KPI"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img45').showModal()"
  >
</p>

<dialog id="img45" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/KPI.png" style="max-width:90vw;">
</dialog>

### Add Time Series Chart

**How do gross sales change over time based on order date?**

- Select the `+ Create a Time Series chart` placeholder --> Available objects --> Drag `ORDER_AMOUNT_EURO` to Measures, and `ORDER_DATE_KEY` to `Time location`  
- Click on the `right side panel` icon from the toolbar to view the chart  
- Click on `1M` in the chart  
- Double click on `ORDER_AMOUNT_EURO per ORDER_DATE_KEY` title and enter `Gross Sales per Order Date` 

<p>
  <img
    src="{{ site.baseurl }}/images/time_series.png"
    alt="time_series"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img46').showModal()"
  >
</p>

<dialog id="img46" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/time_series.png" style="max-width:90vw;">
</dialog>

**Interpretation**: Sales are relatively low at the beginning of January, before increasing and reaching their highest point around mid-January. After this peak, sales continue but fluctuate for the rest of the month. Overall, this suggests that mid-January was the strongest sales period, while the rest of the month shows more variable sales activity.

### Add tables

**What is the relationship between discounts and invoiced revenue across different sales organizations? We use the invoiced revenue measure because it reflects real, finalized sales that have already been billed to customers.**

- Select the `+ Create a Table` placeholder in the Main Lane of the template  
- In the `Builder` tab under `Rows`, select `+ Add Dimension` --> Select `SOLD_TO_CUSTOMER`, `SALES_ORGANIZATION` --> Click outside the Dimension Dropdown to close it  
- Add your column dimensions --> Under `Columns`, select `+ Add Dimension` --> Select `ORDER_DATE_KEY`  
- Change the measure column --> Select `Set Filters for Measures` --> Select `Invoice gross revenue` and `% Discount`  

<p>
  <img
    src="{{ site.baseurl }}/images/table.png"
    alt="table"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img47').showModal()"
  >
</p>

<dialog id="img47" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/table.png" style="max-width:90vw;">
</dialog>

**Interpretation**: Invoiced revenue is different across sales organizations. Some organizations generate much more revenue than others and the level of discounts also varies. This suggests that sales performance is influenced by more than just discount strategies and that some organizations may have stronger customer demand.

### Add Geo Maps

**Where are our customers located, and how is sales activity distributed across regions?**

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

<p>
  <img
    src="{{ site.baseurl }}/images/input_controls.png"
    alt="input_controls"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img48').showModal()"
  >
</p>

<dialog id="img48" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/input_controls.png" style="max-width:90vw;">
</dialog>

### Create page 2 
- Toolbar --> `View` --> `left side panel` --> `Outline` --> `Add second page`  
- Go to `page 2` and click on `Assets` 

**Which customer segments and account types generate the most revenue in France?**

### Pie Chart
- From `widgets`, drag `Chart` in the storyboard page 2  
- Choose data source and the analytic model you created  
- From `Builder panel` --> Selected chart: `Pie`  
- Measures: `France revenue`  
- Dimensions: `CustomerSegment`   
- Double click on the chart title and change it to: `France Revenue Share by Customer Segment` 
<p>
  <img
    src="{{ site.baseurl }}/images/pie_chart.png"
    alt="pie_chart"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img49').showModal()"
  >
</p>

<dialog id="img49" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/pie_chart.png" style="max-width:90vw;">
</dialog>
**Interpretation**: Medium and Low value customers contribute the largest share of revenue in France. This suggests that a significant part of sales comes from customers that are not necessarily classified as the most valuable, meaning they still play an important role in overall revenue.

**In which industries do customers typically pay more per order?**

### Column Chart
- From `widgets`, drag `Chart` in the storyboard page 2   
- From `Builder panel` --> Chart orientation: `Vertical`  
- Measures: `Avg Order Price`  
- Dimensions: `Industry`  
- Color: `Industry`  
- Double click on the chart title and change it to: `Average Order Price by Industry`
<p>
  <img
    src="{{ site.baseurl }}/images/bar_chart.png"
    alt="bar_chart"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img50').showModal()"
  >
</p>

<dialog id="img50" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/bar_chart.png" style="max-width:90vw;">
</dialog>
**Interpretation**: Across most industries, customers pay roughly similar amounts per order. However, in the healthcare industry, customers tend to pay the highest average order price, which may indicate that products sold in this industry are more specialized or higher value.

**Which types of customers buy the most high-value products?**
### Heatmap:
- From `widgets`, drag `Chart` in the storyboard  
- From Builder panel --> Selected chart: `Heatmap`  
- Color: `Expensive products`  
- Dimensions: `qualityscore` (X-axis), `accounttype` (Y-axis)  
<p>
  <img
    src="{{ site.baseurl }}/images/heatmap.png"
    alt="heatmap"
    style="width:600px; cursor:pointer;"
    onclick="document.getElementById('img51').showModal()"
  >
</p>

<dialog id="img51" onclick="if(event.target===this)this.close()">
  <img src="{{ site.baseurl }}/images/heatmap.png" style="max-width:90vw;">
</dialog>
**Interpretation**
- Color intensity → Magnitude  
  - Darker / Blue = higher value  
  - Lighter / Pink = lower value  

The heatmap shows that Monitoring accounts with a quality score of 7 purchase the highest number of expensive products. This suggests that these customers are reliable and actively purchasing higher-value products, making them important for revenue generation.

Account type explanation:
Target – New or potential customers that the company is trying to grow.
Strategic – High-priority customers that are considered very important for the business.
Monitoring – Existing customers that are stable but require observation to maintain or grow the relationship.

**Which customer segments and industries spend the most on average?**
(...)
**The scatter plot shows customer clusters created by the machine learning model, helping identify groups of customers with similar characteristics.**
(...)

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
