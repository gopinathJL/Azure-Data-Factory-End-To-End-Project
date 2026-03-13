# Azure-Data-Factory-End-To-End-Project
Azure Data Factory End-to-End Project – PySpark, Data Migration &amp; Medallion Architecture

This repository demonstrates an end-to-end Azure Data Engineering solution that ingests data from On‑premises SQL, Azure SQL, and REST APIs into Azure Data Lake Storage Gen2 using Azure Data Factory, applies PySpark transformations following the Medallion architecture (Bronze–Silver–Gold), and operationalizes the pipeline with Git/Azure DevOps and Logic Apps–based alerts.

##Project Overview
Sources:
    On‑premises SQL Server via Self‑Hosted Integration Runtime.
    Azure SQL Database.
    External API data (HTTP/JSON).
Ingestion & Orchestration: Azure Data Factory pipelines (full + incremental).
Storage: ADLS Gen2 with Bronze, Silver, and Gold layers.
Transformations: PySpark (Databricks/Spark) notebooks for cleaning, standardization, and modeling.
DevOps: Git/Azure DevOps integration for ADF JSON and notebooks.
Monitoring & Alerts: Azure Logic Apps + ADF alerts to notify on failures and SLA breaches.

Architecture
End-to-end flow:
On‑prem SQL / Azure SQL / API → ADF Pipelines → ADLS Gen2 (Bronze → Silver → Gold using PySpark) → Azure SQL / Synapse / Power BI → Git/Azure DevOps (CI/CD) + Logic Apps alerts.
Bronze Layer:
    Raw ingestion from On‑prem SQL, Azure SQL, and APIs stored as‑is (CSV/Parquet/JSON).
    Maintains full history and supports reprocessing.
Silver Layer:
    PySpark cleans and standardizes schemas across different sources, handles nulls, deduplication, and type casting.
    Conforms data from SQL and APIs into a unified, analytics‑ready structure.
Gold Layer:
    Business-level fact and dimension tables with aggregations and KPIs.
    Exposed to reporting tools and downstream applications.

Alerts with Logic Apps:
To improve observability, ADF is integrated with Logic Apps for automatic notifications.
    ADF pipeline activities use failure paths (On Failure) to trigger a Logic App HTTP endpoint.
    Logic App reads details (pipeline name, run id, error message) and sends email or Teams alerts to the support team.
    Native ADF alert rules are configured to monitor pipeline and trigger failures in the Monitor pane.

DevOps & Git Integration:
    ADF is configured with Git integration (GitHub / Azure DevOps) so that pipelines, datasets, and linked services are version controlled.
    ARM/JSON templates and PySpark notebooks are stored in the repo and deployed via Azure DevOps pipelines using YAML.
    Branching strategy (e.g., feature → develop → main) ensures safe promotion from dev to prod.


