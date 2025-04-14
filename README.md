# End-to-End Healthcare Revenue Data Pipeline 
## Overview
This project implements an end-to-end scalable data engineering pipeline for processing healthcare revenue data using Azure services. The pipeline ingests, processes, and models financial data from healthcare facilities within Azure Databricks, applying a Medallion Architecture (Bronze, Silver, Gold layers) to incrementally refine data quality and structure.

The final Gold layer organizes the data into a well-designed star schema with dimension and fact tables, enabling efficient reporting, analytics, and financial insights for healthcare decision-makers.



## Tech Stack
- **Azure SQL Database (2 sources)** – Source systems containing healthcare revenue and operations data

- **Azure Data Factory (ADF)** – Orchestrates data ingestion from both databases, moves it to ADLS Gen2, and triggers Databricks workflows

- **Azure Data Lake Storage Gen2 (ADLS Gen2)** – Acts as:

  - Landing zone for raw data from both databases

  - Bronze layer for ingested raw data

  - Storage for a central config file (metadata) describing all tables from both databases

- **Azure Databricks (ADB)** – Performs data processing, cleansing, transformation, and modeling using PySpark

- **Azure Key Vault** – Secure storage of credentials and secrets

## Architecture
![image](https://github.com/user-attachments/assets/adb6e400-2914-43cf-a211-9c2e0cc92465)

## Features
- Ingestion from two distinct Azure SQL Databases into a unified, scalable data lake

- Metadata-driven ingestion using a config file stored in ADLS Gen2

- Medallion architecture implemented as:

  - Landing Zone and Bronze in ADLS Gen2

  - Bronze, Silver, and Gold in Azure Databricks
-  Silver Layer Enhancements:
     - Applied a Common Data Model (CDM) structure to maintain consistency and interoperability across datasets

    - Implemented Slowly Changing Dimension (SCD) Type 2 for historical tracking

   

- Star schema design in the Gold layer with dimension and fact tables

- Modular, scalable, and parameterized pipeline design

- Secure credential management via Azure Key Vault

## Process Flow
1. Ingestion:

    - ADF ingests data from:

      - Two Azure SQL Databases

      - Azure Databricks notebook pulls data from public APIs

    - Raw data lands in ADLS Gen2 Landing Zone

2. Metadata Management:
 
    - A config file in ADLS Gen2 stores metadata for both databases and APIs

    - This config drives the ingestion and transformation logic

3. Bronze Layer:

    - Raw data is organized in ADLS Gen2 Bronze layer

    - Partial Bronze processing and API ingestion happen in Azure Databricks

4. Silver Layer:

    - Cleaned, enriched, and transformed data
    
    - Structured data following the Common Data Model (CDM) to ensure consistent schema definitions and standardized naming conventions
    -  Implemented SCD Type 2 for tracking historical changes in dimensional data

5. Gold Layer:

    - Data modeled into a star schema in Databricks:

    - Dimension tables (e.g., Facility, Department, Date, Payment Method)

    - FactRevenue table with aggregated financial metrics

6. Security:

    - Azure Key Vault secures credentials and API keys

7. CI/CD:

    - GitHub for version control and continuous integration


