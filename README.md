# 🛒 E-Commerce Data Integration Pipeline via Azure Data Factory

## 📝 Project Overview
This project showcases an end-to-end Data Engineering pipeline designed to ingest, transform, and load e-commerce data. Built entirely within **Azure Data Factory (ADF)**, the pipeline simulates a real-world scenario of migrating and processing on-premise data to a cloud-based architecture, ensuring data quality and readiness for downstream analytics.

## 🛠️ Tech Stack & Tools
* **Orchestration & ETL:** Azure Data Factory (Pipelines, Datasets, Linked Services)
* **Data Transformation:** ADF Mapping Data Flows (No-code/Low-code Spark processing)
* **Compute / Connectivity:** Self-Hosted Integration Runtime (SHIR)
* **Storage / Sink:** Azure Data Lake / Parquet format
* **Version Control:** Git Integration (GitHub) for CI/CD pipelines

## 🏗️ Pipeline Architecture

### 1. Data Ingestion (On-Premise to Cloud)
* Configured a **Self-Hosted Integration Runtime (SHIR)** to securely bypass local firewall restrictions and extract raw flat files (CSV) directly from an on-premise machine.
* Utilized parameterized **Linked Services** to establish robust and secure connections.

### 2. Data Transformation (Mapping Data Flows)
Implemented complex transformation logic to clean and standardize the dataset:
* **Schema Drift & Select:** Renamed and mapped columns to fit the target data warehouse standards.
* **Handling Nulls & Data Imputation:** Engineered a dynamic derived column to handle missing values. 
* **Advanced Logic (SCD Type 2 Simulation):** Instead of static values, created a dynamic mathematical expression utilizing hashing and UUIDs to generate randomized, unique future expiration dates for product records:
  `addDays(toDate('2025-01-01'), toInteger(abs(crc32(uuid())) % 1460))`

### 3. Data Sink & Storage
* Exported the final, transformed dataset into **Parquet** format to optimize storage cost and maximize query performance for future BI tools.

### 4. CI/CD & Source Control (Git-backed Authoring)
* Integrated the ADF workspace with GitHub.
* Replaced live-mode manual publishing with a robust **Save All** workflow to the `main` branch, applying enterprise-level DevOps and code management best practices.

## 📸 Execution & Monitoring Screenshots

### Pipeline Architecture Overview
<img width="1920" height="1080" alt="Screenshot (316)" src="https://github.com/user-attachments/assets/1ff455e3-319b-4225-952a-f23e2afc43b6" />


### Transformation Logic (Expression Builder)
<img width="1920" height="1080" alt="Screenshot (313)" src="https://github.com/user-attachments/assets/de19dece-afa3-4d71-952b-94b25c8337e5" />

<img width="1920" height="1080" alt="Screenshot (314)" src="https://github.com/user-attachments/assets/bac3e488-53e4-4aeb-8f22-0b79c75f8dc0" />

### Successful Execution (Monitor Tab)
<img width="1920" height="1080" alt="Screenshot (315)" src="https://github.com/user-attachments/assets/bc517ac0-de3a-44da-b490-6b9f3c050e1d" />
