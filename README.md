# Event-Driven Orders Data Load Project (Databricks + PySpark)

This project implements an **event-driven ETL pipeline** to ingest and transform **order data** using **Databricks**, **PySpark**, and **cloud storage**. It is split into two main stages: **Staging Load** and **Target Load**, following a modular data pipeline structure.

---

## 📁 Project Structure

- `orders_stage_load.ipynb`  
  Reads raw event data from source (e.g., cloud storage), performs initial parsing/validation, and stages it for downstream transformation.

- `orders_target_load.ipynb`  
  Consumes the staged data, applies business logic (e.g., type casting, filtering, enrichment), and loads the cleansed data into a final data warehouse/table.

---

## 🚀 Features

- Event-driven architecture using notebook triggers or workflow jobs.
- PySpark-based scalable data transformations.
- Schema inference and data validation.
- Modular ETL design for better debugging and reusability.
- Suitable for batch or streaming extensions.

---

## 🧱 Technologies Used

- [Databricks](https://www.databricks.com/)
- PySpark
- Delta Lake / Unity Catalog
- Cloud Storage (e.g., AWS S3 or GCP GCS)
- GitHub for version control

---

## 🔧 How to Run

1. **Upload notebooks** to your Databricks workspace.
2. Update the required configs:
   - Source/target path
   - Table/database names
   - Credentials if accessing cloud storage 
3. Run `orders_stage_load.ipynb` to ingest and stage raw data.
4. Run `orders_target_load.ipynb` to transform and load it into the final table.

> 📝 These notebooks can also be scheduled using **Databricks Workflows** or triggered using **Databricks Jobs API**.

---

## 📌 Example Use Case

Imagine a system that drops raw order files into cloud storage. This project picks up those files automatically, loads them to a staging layer, applies business logic, and makes them available for analytics teams or dashboards.

---
## 🔒 Security

- **Avoid using default workspace credentials** like `'gds_learning'` when accessing external storage in Unity Catalog. These are **restricted to specific paths**, for example:
**gs://databricks-<workspace-id>-unitycatalog/<workspace-id>**
- ❗ Using default credentials to access other paths will result in this error:

com.databricks.sql.managedcatalog.acl.UnauthorizedAccessException: PERMISSION_DENIED:
The credential 'gds_learning' is a workspace default credential that is only allowed to access data in the following paths: 


### ✅ Solution

To resolve this, follow these steps:

1. Create a new external location and credential in Unity Catalog with appropriate permissions.
2. Grant access to users, groups, or service principals.
3. Use this external location in your notebooks or data pipeline for reading/writing data.

💡 Ensure the cloud service account used in the credential has sufficient IAM permissions to access the given bucket/path.

---
