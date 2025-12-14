# 📥 Phase 1: Data Ingestion

## 🎯 Objective
To securely extract raw data from an on-premise **MySQL database** and ingest it into the **AWS S3 Landing Zone** without data loss.

## ⚙️ Workflow
1.  **Connection:** A Python script connects to the local MySQL instance using `mysql-connector-python`.
2.  **Extraction:** Reads the `support_tickets` and `support_logs` tables into Pandas DataFrames.
3.  **Upload:** Uses `boto3` to upload raw CSV files to the S3 bucket organized by folders (`raw/tickets/`, `raw/logs/`).

## 🔑 Key Challenges Solved
* **Security:** Database credentials are managed via environment variables (`.env`) and never hardcoded.
* **Automation:** The script automatically creates the S3 bucket structure if it doesn't exist.

## 🚀 How to Run
1.  Install dependencies: `pip install -r ../requirements.txt`
2.  Configure `.env` file with MySQL and AWS credentials.
3.  Run the notebooks: `support_logs_ingestion_to_S3.ipynb`, `support_tickets_ingestion_to_S3.ipynb`
