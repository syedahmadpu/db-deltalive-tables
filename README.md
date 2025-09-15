# End-to-End ETL Pipeline with Databricks & Delta Live Tables

This project demonstrates a complete, production-style ETL pipeline built on the Databricks Lakehouse Platform. It processes raw e-commerce data from a fictional company, "circuitbox," through a Medallion Architecture (Bronze, Silver, Gold) to produce clean, reliable data ready for BI and AI workloads.

---

## Data Architecture

The project follows the modern Data Lakehouse paradigm, using Azure Data Lake Storage (ADLS) Gen2 for storage and Databricks for compute and governance. All data assets are governed by Unity Catalog.



---

## Key Features Implemented

* **Medallion Architecture:** Data is logically organized into Bronze (raw), Silver (cleaned), and Gold (aggregated) layers.
* **Delta Live Tables (DLT):** The entire ETL pipeline is defined declaratively using DLT with both SQL and PySpark notebooks.
* **Unity Catalog Governance:** All data assets (catalogs, schemas, tables, volumes) are managed and secured by Unity Catalog.
* **Auto Loader for Ingestion:** Raw files (JSON & CSV) are incrementally and efficiently ingested from cloud storage using Auto Loader, with features like schema inference and data rescue.
* **Data Quality Enforcement:** DLT Expectations are used to define and enforce data quality rules, allowing for dropping, quarantining, or failing on bad records.
* **Change Data Capture (CDC):** The `APPLY CHANGES INTO` API is used to handle updates, inserts, and deletes.
* **Slowly Changing Dimensions (SCD):** Implemented both SCD Type 1 (overwrite) and SCD Type 2 (history tracking) for dimension tables.
* **Optimized Aggregations:** A **Materialized View** is used in the Gold layer to serve pre-computed, low-latency results for BI dashboards.
* **Production Orchestration:** A **Databricks Workflow (Job)** is configured to schedule and automate the end-to-end DLT pipeline runs.

---

## Technology Stack

* **Platform:** Databricks
* **Storage:** Azure Data Lake Storage (ADLS) Gen2
* **Data Format:** Delta Lake
* **Governance:** Unity Catalog
* **Ingestion:** Auto Loader
* **Pipeline Framework:** Delta Live Tables (DLT)
* **Languages:** SQL, Python (PySpark)

---

## How to Run

1.  **Setup Cloud Storage:** Ensure the raw data files are present in the designated ADLS Gen2 landing zone folders.
2.  **Configure Unity Catalog:** Create the necessary Catalogs, Schemas, and External Locations as defined in the setup notebooks.
3.  **Create DLT Pipeline:** In the Databricks UI, create a new Delta Live Tables pipeline, linking the source code notebooks from this repository.
4.  **Configure and Run:** Set the target schema in the pipeline configuration and start the pipeline. It will automatically build the dependency graph and process the data through the Bronze, Silver, and Gold layers.
5.  **Schedule (Optional):** To automate the pipeline, create a Databricks Job that is triggered on a schedule and points to this DLT pipeline.

---
