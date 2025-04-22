# 🏡 Zillow Data Analytics — End-to-End Data Engineering Project

This project demonstrates a complete **end-to-end data engineering pipeline** on the AWS Cloud, focused on real estate data from the **Zillow Rapid API**. The goal is to automate data extraction, transformation, loading, and analysis using Python, AWS services, and Apache Airflow.

---

## 🚀 Project Overview

- **Source**: Zillow Rapid API
- **Orchestration**: Apache Airflow (on EC2)
- **Data Pipeline**:
  - Extract API data using Python
  - Load raw JSON to Amazon S3
  - Use AWS Lambda functions to copy and convert JSON → CSV
  - Store cleaned CSV in final S3 bucket
  - Load data to Amazon Redshift
  - Visualize insights with Amazon QuickSight

---

## 📦 Architecture

```
Zillow Rapid API → Python Script → S3 (raw) → Lambda (copy) → S3 (intermediate) → Lambda (transform) → S3 (cleaned) → Airflow DAG → Redshift → QuickSight
```

---

## 🛠️ Tech Stack

- **Languages**: Python, Bash
- **AWS Services**: S3, Lambda, Redshift, IAM, EC2, QuickSight
- **Orchestration**: Apache Airflow (S3KeySensor, PythonOperator, S3ToRedshiftOperator)
- **Transformation**: Pandas, JSON, CSV
- **Visualization**: Amazon QuickSight

---

## 📁 Repository Structure

```
zillow-data-analytics/
│
├── dags/
│   └── zillow_dag.py               # Airflow DAG (Python)
│
├── lambda_functions/
│   ├── copy_raw_json.py           # Lambda to copy file to intermediate bucket
│   └── transform_to_csv.py        # Lambda to convert JSON → CSV
│
├── config/
│   └── config_api.json            # Zillow API headers (not included in repo for security)
│
├── screenshots/                   # (Optional) Dashboards, architecture, Airflow UI
│
├── requirements.txt               # Python packages used
└── README.md                      # Project documentation
```

---

## 🔁 Workflow Details

1. **Data Extraction**
   - A Python script (triggered by Airflow) hits the Zillow Rapid API.
   - Response JSON is saved locally and pushed to the raw S3 bucket.

2. **Lambda Triggers**
   - **Lambda 1**: Automatically copies the raw JSON to a secondary S3 bucket.
   - **Lambda 2**: Converts the copied JSON into CSV using Pandas and pushes to a final S3 bucket.

3. **Data Pipeline Orchestration**
   - **Airflow DAG**:
     - Executes Python extraction task.
     - Uses BashOperator to move file to S3.
     - Waits for transformed file using S3KeySensor.
     - Loads CSV from S3 into Redshift using S3ToRedshiftOperator.

4. **Data Analysis**
   - Connect Amazon Redshift to Amazon QuickSight.
   - Build interactive dashboards for real estate insights.

---

## 📊 Sample Dashboard

> *(Optional: Add screenshots in the `screenshots/` folder and reference them here)*

---

## 🔐 Security

- Sensitive credentials like API keys and IAM roles are securely stored and not shared in this repository.

---

## ✅ Future Improvements

- Schedule Lambda via EventBridge instead of relying solely on S3 triggers.
- Integrate CI/CD for deployment via GitHub Actions.
- Add data quality checks before Redshift ingestion.

---

## 📬 Contact

If you found this helpful or have any questions, feel free to connect!

---
