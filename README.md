# 🔁 Kafka-Based Real-Time Streaming Pipeline  
[Project Files & Demo](https://drive.google.com/file/d/1ctwK0Lp9H0Z_lg3QeA6-SEqZM7keGBky/view?usp=sharing)

## 📌 Project Overview

This project demonstrates an end-to-end real-time data streaming pipeline using **Apache Kafka** deployed on an **AWS EC2 instance**, with live stock market data streamed from a producer to a consumer and then pushed to **Amazon S3** for analysis using **AWS Athena**. The pipeline simulates production-grade streaming, cloud integration, and automation-ready analytics.

---

## ⚙️ Architecture & Flow

- **Apache Kafka** and **Zookeeper** deployed on a public EC2 server
- **Kafka Producer** in Jupyter Notebook streaming records from a stock market CSV
- **Kafka Consumer** receives live data and writes to Amazon S3 in JSON/Parquet format
- **AWS Glue Crawler** catalogs S3 data
- **Amazon Athena** queries and analyzes near real-time data
- Option to add **EventBridge** and **Step Functions** for automation

---

## ⚠️ Issues Faced and How I Solved Them

### 🔐 1. EC2 SSH Connection Error
- **Problem:** Couldn’t SSH into EC2 due to permission denied errors.
- **Fix:** Applied `chmod 400` to the key file and connected successfully.

### 🌐 2. Kafka Server Not Exposing Public IP
- **Problem:** Kafka wouldn’t accept external connections.
- **Fix:** Modified `server.properties` to advertise the EC2 public IP. Also updated Zookeeper settings and EC2 security group inbound rules.

### 📉 3. EC2 Performance Bottlenecks
- **Problem:** Kafka crashed when handling large data due to limited compute.
- **Fix:** Resized the EC2 instance to a compute-optimized type.

### 💾 4. AWS S3 Upload Fails from Jupyter
- **Problem:** Couldn’t write data to S3 from the local notebook.
- **Fix:** Created a programmatic IAM user, configured AWS CLI, installed `s3fs`, and authenticated locally using access keys.

### 🧮 5. Athena Query Errors
- **Problem:** Athena wouldn’t return results due to missing query result path.
- **Fix:** Configured a dedicated S3 results folder and used Parquet format to reduce query scan time.

---

## 💡 Key Learnings

- Implemented real-time data flow with end-to-end visibility from producer to query
- Used **Parquet + Snappy compression** to optimize both S3 cost and Athena speed
- Secured AWS access via IAM and minimized exposure using EC2 firewall controls
- Built scalable logic with `sleep()` throttling and batch-based ingestion
- Designed the pipeline to be automation-ready using DAGs and Step Functions

---

## 📂 Technologies Used

- Apache Kafka, Zookeeper, EC2
- Jupyter Notebook (Producer & Consumer)
- AWS S3, IAM, CLI
- AWS Glue, Athena
- Parquet, JSON, pandas

---

## 📎 Project Files

You can explore the full setup, codebase, and screenshots [here in Google Drive](https://drive.google.com/file/d/1ctwK0Lp9H0Z_lg3QeA6-SEqZM7keGBky/view?usp=sharing).

