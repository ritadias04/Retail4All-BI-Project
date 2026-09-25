# Retail4All – End-to-End Business Intelligence Solution

Business Intelligence project developed at NOVA IMS (Master's in Data Science and Advanced Analytics). Final grade: 17.42.

## Business Problem
Retail4All is a Portuguese retail company with a network of physical and online stores and three years of daily transactional data. It had no centralised system to analyse sales trends, compare years or track performance by store, product, operator or location. The goal was to build a complete BI solution, from raw data to an interactive self-service report.

## Business Questions
- What are the total revenue and units sold by product category across months, quarters and years?
- Which operators generate the highest sales over time?
- Which points of supply generate the majority of total sales?
- How does sales volume differ between physical and online stores over time?
- Which locations drive the highest revenue and growth?

## Solution Architecture (Microsoft Fabric)
1. **Dimensional model:** designed with the Kimball methodology as a star schema, with a central sales fact table and dimensions for date, product, store, location, operator and point of supply.
2. **ETL:** data ingested into a Lakehouse, transformed with Dataflows and loaded into a Data Warehouse, with referential integrity maintained at every stage.
3. **Pipeline orchestration:** a single pipeline loads all dimensions first, then the fact table.
4. **Incremental load:** the sales fact table uses incremental refresh with quarterly partitions, so only new or modified records are reprocessed on each run.
5. **Monitoring:** email notifications for pipeline success or failure.
6. **Advanced analytics:** a Python notebook, run inside the pipeline, segments stores with **K-Means** (one-hot encoding, scaling, elbow method, PCA visualisation) and writes the clusters back to the warehouse as a new dimension.

## Reporting Layer (Power BI)
- **Semantic model** with hierarchies, data types, formatting and relationships.
- **DAX measures**, including time-intelligence calculations such as Revenue YoY % and operator rankings by year.
- **Interactive report** organised into thematic pages, each with its own narrative:
  - Executive Overview
  - Product Performance
  - Operator Performance
  - Channels and Supply Points
  - Location and Business Drivers
