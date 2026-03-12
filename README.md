# 📡 IoT Sensor Anomaly Detection Pipeline

## 🚀 Project Overview
This project builds a **real-time IoT data engineering pipeline** to monitor sensor data, detect anomalies, and generate operational insights for predictive maintenance.

The pipeline ingests IoT sensor streams, processes them using **PySpark on Databricks**, stores them using **Delta Lake Medallion Architecture**, and produces analytics-ready datasets.

### Key Capabilities
- Real-time IoT data ingestion
- Data quality validation and cleansing
- Sensor anomaly detection using statistical methods
- Delta Lake storage with Bronze → Silver → Gold architecture
- Aggregated device performance analytics
- Alert generation for abnormal sensor behavior

---

# 🏗️ Architecture / ETL Pipeline Flow

```
IoT Sensor JSON Events (Amazon Kinesis)
             ↓
Databricks Streaming Ingestion
             ↓
Bronze Layer (Raw Data)
iot_catalog.raw.sensor_readings
             ↓
Data Cleaning & Validation
             ↓
Silver Layer (Processed Data)
iot_catalog.processed.valid_readings
             ↓
Anomaly Detection & Aggregations
             ↓
Gold Layer (Analytics Tables)
iot_catalog.analytics.device_stats
             ↓
Monitoring Dashboards & Alerts
```

Pipeline follows **Medallion Architecture** for scalable data processing.

---

# 🛠️ Tech Stack

| Technology | Purpose |
|------------|--------|
| Databricks | Data Engineering Platform |
| PySpark | Distributed Data Processing |
| Delta Lake | Reliable Data Storage |
| Amazon Kinesis | Real-time IoT data streaming |
| AWS S3 | Raw data storage |
| Unity Catalog | Data governance |
| Slack | Alert notifications |
| GitHub | Version control |

---

# 📂 Project Structure

```
IoT-Anomaly-Pipeline/
│
├── datasets/                     # IoT sensor datasets
├── notebooks/
│   ├── 01_ingestion_bronze.py
│   ├── 02_transformation_silver.py
│   └── 03_anomaly_detection_gold.py
│
├── schemas/                      # JSON schema definitions
├── sql/                          # Analytics SQL queries
├── configs/                      # Pipeline configurations
├── images/                       # Architecture diagrams
├── tests/                        # Unit tests
│
├── requirements.txt
└── README.md
```

---

# 📌 Problem Statement

Modern IoT systems generate **high-volume streaming sensor data** that must be continuously monitored to detect abnormal patterns.

This pipeline solves the following problems:

### 🔹 Real-Time Monitoring
- Ingest IoT sensor data from streaming sources
- Process high-velocity sensor readings

### 🔹 Data Quality Validation
- Remove corrupted records
- Validate sensor ranges

### 🔹 Anomaly Detection
- Identify abnormal temperature or humidity values
- Detect device malfunctions early

### 🔹 Predictive Maintenance
- Identify failing sensors before downtime occurs

---

# ⚙️ Business Rules Implemented

## 1️⃣ Data Quality Validation

| Field | Rule |
|------|------|
| temperature | Must be within valid sensor range |
| humidity | Must be between 0–100 |
| device_id | Cannot be null |
| timestamp | Must contain valid event time |

Invalid records are filtered during the **Silver transformation stage**.

---

## 2️⃣ Sensor Reading Validation

```
temperature > -50 AND temperature < 150
humidity >= 0 AND humidity <= 100
pressure > 0
```

Invalid sensor readings are discarded or logged.

---

## 3️⃣ Anomaly Detection Logic

Anomalies are detected using **Z-score statistical method**.

```
z_score = (value - mean) / stddev
```

| Condition | Status |
|-----------|--------|
| z_score > 3 | ANOMALY |
| z_score < -3 | ANOMALY |
| Otherwise | NORMAL |

---

# 📊 Key Metrics Calculated

The pipeline generates multiple analytical metrics:

- Sensor temperature averages
- Humidity trends
- Device performance statistics
- Rolling 5-minute averages
- Anomaly rate per device
- Sensor health indicators

---

# 📊 Data Model

### Dimension Tables

**dim_sensor_master**

**dim_device**

**dim_environment**

**dim_time**

---

### Fact Table

**fact_sensor_readings**

---

# 📊 Analytics Queries

### 🔹 Devices With Highest Anomaly Rate

---

### 🔹 Average Sensor Temperature

---

### 🔹 Anomaly Rate by Location

---

# ⚡ Streaming Configuration

Pipeline runs using **Databricks Structured Streaming**.

| Setting | Value |
|------|------|
| Trigger Mode | Micro-batch |
| Batch Interval | 10 seconds |
| Checkpointing | Enabled |
| Fault Tolerance | Delta Lake |

---

# 🔔 Alerting & Monitoring

The pipeline generates alerts when anomaly rates exceed thresholds.

Alert mechanisms include:

- Slack notifications for anomaly spikes
- Logging errors to `anomaly_log` table
- Databricks job monitoring

---

# 🧪 Testing Strategy

Pipeline validation includes:

- Unit tests for anomaly detection logic
- Schema validation tests
- Batch validation with Kaggle IoT datasets
- QA approval before production deployment

---

# 🧮 How to Run This Project

## 1️⃣ Clone Repository

```bash
git clone https://github.com/Mahendermaahi/-IoT-Sensor-Anomaly-Detection-Pipeline
cd iot-anomaly-pipeline
```

---

## 2️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 3️⃣ Configure Databricks

Create a cluster with the following configuration:

```
Node Type: m5.xlarge
Workers: 8 – 32
Runtime: Databricks Runtime for Apache Spark
Libraries:
- pyspark
- delta-spark
- aws-kinesis-spark
```

---

## 4️⃣ Run Databricks Notebooks

Execute notebooks in the following order:

```
01_ingestion_bronze
02_transformation_silver
03_anomaly_detection_gold
```

---

# 📦 requirements.txt

```
pyspark
delta-spark
aws-kinesis-spark
pandas
numpy
matplotlib
seaborn
```

---

# 📈 Outcome

This project demonstrates:

- Scalable real-time IoT data pipeline
- Clean and validated sensor datasets
- Automated anomaly detection
- Delta Lake optimized storage
- Analytical tables for monitoring dashboards

---

# 🚀 Future Enhancements

Planned improvements:

- Machine learning anomaly detection models
- Predictive maintenance using ML
- Real-time dashboards using Streamlit
- Apache Airflow orchestration
- Integration with live IoT device APIs

---

# 👨‍💻 Author

**Mahender Reddy Lyagala**

Data Engineering | Big Data | IoT Analytics | PySpark | SQL | Cloud Data Platforms

---

# ⭐ Support

If you found this project helpful, give it a ⭐ on GitHub!
