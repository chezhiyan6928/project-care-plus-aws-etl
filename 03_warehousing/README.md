# 🏛️ Phase 3: Data Warehousing & Analysis

## 🎯 Objective
To load processed data into a Data Warehouse (**Amazon Redshift**) and enable ad-hoc querying via **AWS Athena**.

## 📊 Data Warehousing (Redshift)
We implemented a **Star Schema** approach where appropriate, though currently flattened for performance.

* **Loading Strategy:** Used the `COPY` command to bulk load data from S3 to Redshift. This is significantly faster than row-by-row insertion.
* **Tables Created:**
    * `dim_tickets`: Dimension attributes for tickets.
    * `fact_logs`: System performance metrics.

## 🔍 Ad-Hoc Analysis (Athena)
AWS Athena was used to run SQL queries directly on S3 files before loading them into Redshift. This allowed for quick data quality checks.

**Sample Query (Average Response Time by Agent):**
```sql
SELECT
    t.agent,
    AVG(l.response_time) as avg_response_ms
FROM support_tickets t
JOIN support_logs l ON t.ticket_id = l.ticket_id
GROUP BY t.agent
ORDER BY avg_response_ms DESC;
