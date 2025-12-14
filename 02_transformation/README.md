# 🔄 Phase 2: Data Transformation

## 🎯 Objective
To clean, standardize, and transform raw data into a query-optimized format.

## 🏗️ Hybrid Architecture
We used a hybrid approach for transformation to optimize for cost and performance:

### 1. Processing Support Logs (Lightweight) -> **AWS Lambda**
* **Why Lambda?** The logs are event-based JSON/CSV files that arrive frequently. Lambda is cost-effective for small, trigger-based processing.
* **Action:** Triggered on S3 upload. It parses the log date, adds a `process_date` column, and converts the file to a clean format.

### 2. Processing Support Tickets (Heavy) -> **AWS Glue**
* **Why Glue?** The tickets dataset is relational and requires complex joining, deduplication, and schema validation.
* **Action:** A **PySpark** job reads the data, handles missing values (imputing `resolved_at` for open tickets), and repartitions the data for efficient storage.

## 🧹 Transformations Applied
* **Date Standardization:** Converted string timestamps to standard `timestamp` format.
* **Data Typing:** Cast `response_time` and `cpu` to numerical types for aggregation.
* **Handling Nulls:** Replaced null `resolved_at` dates with a placeholder for analysis.
