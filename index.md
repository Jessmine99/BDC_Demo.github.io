---
title: Introduction
layout: default
nav_order: 1
---
# "Custom" Data Products, Modeling and SAC Reporting

This hands-on demo shows how to build an **end-to-end sales analytics solution** using **SAP Datasphere, SAP Databricks, and SAP Analytics Cloud**.

You will ingest operational sales data, enrich it with external customer data, model it for analytics, and build an interactive dashboard to explore business insights.

The final result is a **sales analytics dashboard** that allows users to analyze revenue trends, customer performance, and product activity through charts, tables, and geo maps.

---

# Objectives

The objective of this demo is to demonstrate how to build an **end-to-end analytics scenario** using key SAP Business Data Cloud components.

During this exercise you will:

- Ingest and manage datasets in **SAP Datasphere**
- Process external data using **SAP Databricks**
- Publish a data product using **Delta Sharing**
- Build fact and dimension models using graphical data modeling
- Define semantic relationships between datasets
- Create an **Analytic Model** for reporting
- Define calculated and restricted measures
- Build an interactive analytics story in **SAP Analytics Cloud**
- Explore data using **Just Ask** and **Data Analyzer**

---

![Architecture overview]({{ site.baseurl }}/images/E2E-scenario.png)

---

# Outcomes

After completing this demo, you will be able to:

- Understand the **end-to-end analytics workflow** across SAP Datasphere, SAP Databricks, and SAP Analytics Cloud
- Perform **data ingestion and preparation** in SAP Datasphere
- Integrate **external data sources** through SAP Databricks
- Design **fact and dimension models** for analytics
- Create **analytic models optimized for reporting**
- Build **interactive dashboards** with charts, tables, and geo maps
- Use filters and input controls for **dynamic analysis**
- Explore insights using **natural language queries with Just Ask**

---

# Scenario

A global company wants to improve its **sales analytics capabilities** by building a unified data and analytics solution.

The company collects operational data such as **sales orders, customer information, and product materials**, but business users lack clear insights into questions like:

- How revenue evolves over time  
- Which customers and regions drive sales performance  
- Which products generate the most value  
- How customers differ in their purchasing behavior  

To address this challenge, the analytics team builds an integrated analytics solution using **SAP Business Data Cloud**.

---

{: .no_toc .text-delta }

<button class="btn js-toggle-dark-mode">Preview dark color scheme</button>

<script>
const toggleDarkMode = document.querySelector('.js-toggle-dark-mode');

jtd.addEvent(toggleDarkMode, 'click', function(){
  if (jtd.getTheme() === 'dark') {
    jtd.setTheme('light');
    toggleDarkMode.textContent = 'Preview dark color scheme';
  } else {
    jtd.setTheme('dark');
    toggleDarkMode.textContent = 'Return to the light side';
  }
});
</script>

---


