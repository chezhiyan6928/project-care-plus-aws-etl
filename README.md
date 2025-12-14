# 🏥 Project Care Plus | End-to-End Data Engineering Pipeline on AWS

## 🚀 Project Overview
**Project Care Plus** is a cloud-native data engineering solution built to process and analyze customer support data for an e-commerce platform.

The goal was to move away from a traditional on-premise database (MySQL) to a scalable **AWS Data Lakehouse architecture**. This pipeline ingests raw data, transforms it using serverless compute, and warehouses it for analytics, enabling business insights into support ticket resolution and system performance.

This project was built as a Capstone Project for the **Codebasics Data Engineering Bootcamp**.

---

## 🏗️ High-Level Architecture
![Pipeline Architecture](./architecture/aws_project_pipeline.svg)

The pipeline flows through three distinct phases:
1.  **Ingestion:** Python scripts extract data from on-prem MySQL to **AWS S3**.
2.  **Transformation:**
    * **AWS Lambda** processes real-time system logs.
    * **AWS Glue (PySpark)** handles heavy batch processing for support tickets.
3.  **Warehousing:** Data is loaded into **Amazon Redshift** for OLAP and queried via **AWS Athena**.

---

## 🗂️ Data Schema
The pipeline processes two related datasets.

### 1. Support Tickets (`support_tickets`)
*Fact table tracking the lifecycle of customer issues.*
| Column | Description |
| :--- | :--- |
| `ticket_id` | Unique ID (PK). e.g., TCK0701011. |
| `status` | Current state (Resolved, Open, Escalated). |
| `priority` | Issue severity (Low, Medium, High). |
| `agent` | Support agent assigned. |
| `created_at` | Timestamp of issue creation. |

### 2. Support Logs (`support_logs`)
*System logs capturing backend events linked to tickets.*
| Column | Description |
| :--- | :--- |
| `log_id` | Unique Log ID. |
| `ticket_id` | Foreign Key linking to `support_tickets`. |
| `log_level` | Severity (INFO, ERROR). |
| `response_time` | API response time (ms). |
| `cpu` | CPU load percentage during the event. |

**Relationship:** One Ticket (1) ↔ Many Logs (N)

---

## 🛠️ Tech Stack
* **Language:** Python (PySpark, Boto3, Pandas), SQL
* **AWS Services:** S3, Lambda, Glue, Redshift, Athena, IAM, CloudWatch
* **Source:** MySQL Database

---

## 📂 Repository Structure
* `01_ingestion/`: Scripts for moving data from On-Prem to Cloud.
* `02_transformation/`: Serverless ETL logic using Lambda and Glue.
* `03_warehousing/`: Data warehousing scripts for Redshift and Athena.
