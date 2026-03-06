---
title: Introduction
layout: default
nav_order: 1
---

# Introduction

End-to-end sales analytics demo using SAP Datasphere, SAP Analytics Cloud and SAP Databricks.  
In this hands-on scenario, you will build an analytics workflow by ingesting, modeling, and enriching data, then visualizing insights through interactive dashboards.

The demo walks through the complete lifecycle of analytics development:
- Data ingestion and preparation
- Data modeling using fact and dimension views
- Creation of an analytic model
- Dashboard creation and exploration
- Enrichment with external Salesforce data

The final result is an interactive sales analytics dashboard that enables users to explore revenue trends and customer performance using charts, tables and geo maps.

---

# Objectives

The objective of this demo is to demonstrate how to build an end-to-end analytics scenario using key SAP Business Data Cloud components.

During this exercise you will:

- Ingest and manage datasets in **SAP Datasphere**
- Build fact and dimension models using graphical data modeling
- Define semantic relationships between datasets
- Create an **Analytic Model** for business reporting
- Define calculated, restricted, and exception aggregation measures
- Create an interactive analytics story in **SAP Analytics Cloud**
- Explore data using **Just Ask** and **Data Analyzer**
- Process external data using **SAP Databricks**
- Publish a data product using **Delta Sharing**
- Enrich analytics models with external Salesforce account data

---

# Outcomes

After completing this demo, you will be able to:

- Understand the end-to-end analytics workflow across SAP Datasphere, SAP Analytics Cloud, and SAP Databricks
- Perform data ingestion and preparation in SAP Datasphere
- Design fact and dimension models with associations and hierarchies
- Create analytic models optimized for reporting
- Build interactive dashboards with charts, tables, and geo maps
- Apply filters and input controls for dynamic analysis
- Use natural language analytics with **Just Ask**
- Integrate external data sources through SAP Databricks
- Extend analytics models with additional business attributes

---

# Scenario

A global company wants to improve its sales analytics capabilities by building a unified data and analytics solution.

The company currently stores operational sales data including:

- Sales orders
- Customer information
- Product materials

However, business users need better insights into:

- Revenue trends over time
- Customer performance across regions
- Product sales performance
- High-value transactions
- Customer segmentation

To address this challenge, the analytics team builds a modern analytics solution using SAP Business Data Cloud technologies.

First, operational datasets are ingested into **SAP Datasphere**, where the team creates a semantic data model consisting of fact and dimension views. These datasets are connected using associations to build a structured model for analysis.

Next, an **Analytic Model** is created to expose business measures such as revenue, discounts, and order metrics.

The analytic model is then consumed in **SAP Analytics Cloud**, where an interactive sales analytics dashboard is created with KPIs, charts, tables, and geo maps.

To enrich the analysis further, external customer account data from **Salesforce** is processed in **SAP Databricks**. The data is transformed and published as a data product using Delta Sharing.

Finally, the enriched data is integrated into the existing customer model in SAP Datasphere, allowing the dashboard to analyze sales performance by additional attributes such as account type, industry, and quality score.

This enables business users to gain deeper insights into customer behavior, identify high-value opportunities, and support data-driven decision making.

![E2E scenario](https://github.com/Jessmine99/BDC_Demo.github.io/blob/main/images/E2E%20scenario.png)
