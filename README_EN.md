# 🛒 E-Commerce Data Pipeline | Azure Databricks & Medallion Architecture

This project consists of building an end-to-end data engineering pipeline using the **Medallion Architecture** (Raw, Bronze, Silver, and Gold) to process and analyze e-commerce data. The solution was developed in **Azure Databricks** using **PySpark** and **Delta Lake**, integrated with **Azure Data Lake Storage Gen2 (ADLS Gen2)**.

---

## 🏗️ Project Architecture

The data flow follows a layered structure to ensure governance, quality, and high performance for analytics consumption:

1. **Raw Layer (ADLS Gen2):** Raw storage of source CSV files uploaded to the Data Lake.
2. **Bronze Layer (Delta Lake):** Ingestion of data into Delta Lake format, preserving the original structure without schema changes.
3. **Silver Layer (Delta Lake):** Data processing, handling null values, deduplication, and data type standardization.
4. **Gold Layer (Delta Lake):** Business-oriented data aggregation (revenue KPIs, order volume by country, and customer spending profiles).

---

## 🛠️ Technologies Used

* **Cloud:** Microsoft Azure (Azure Data Lake Storage Gen2)
* **Data Processing:** Azure Databricks, PySpark, Spark SQL
* **Storage Format:** Delta Lake
* **Language:** Python

---

## 📁 Notebooks Structure

* `01_Ingestao_Bronze.py`: Connection to ADLS Gen2, reading raw CSV files, and initial writing to the Bronze layer in Delta format.
* `02_Transformacao_Silver.py`: Reading from the Bronze layer, cleaning invalid records (null `InvoiceNo` and `CustomerID`), date/time conversion, and writing to the Silver layer.
* `03_Agregacao_Gold.py`: Reading cleaned data from Silver and generating analytical business views (revenue by country and customer metrics).

---

## 🔒 Security Note & Best Practices

For security reasons and **DevSecOps** best practices, access keys (`Storage Account Access Keys`) have been omitted from the public notebooks in this repository. In production environments, it is recommended to use **Azure Key Vault** integrated with **Databricks Secrets** to manage credentials securely.

---

## 🚀 How to Run This Project

1. Create a **Storage Account** in Azure with **Data Lake Storage Gen2** enabled, containing `raw`, `bronze`, `silver`, and `gold` containers.
2. Set up an **Azure Databricks** workspace and create a compute cluster.
3. Import the notebooks from this repository into your Databricks workspace.
4. Insert your Azure access credentials in the `storage_account_access_key` parameter (or configure Databricks Secrets).
5. Execute the notebooks sequentially (`01` ➔ `02` ➔ `03`).
