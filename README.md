# **Sales and Customer Data Processing Pipeline**

## **General Description**

This project demonstrates a scalable and automated **Data Engineering Pipeline** that processes raw sales and customer data into meaningful datasets for analytics and reporting. The pipeline integrates various tools and technologies to fetch data, validate it, transform it according to business requirements, and store the results in structured databases and data lakes for downstream consumption.

The pipeline is designed for batch processing of sales and customer data, ensuring quality checks, business rule implementations, and optimized storage for querying and reporting purposes.

---

## **Purpose of the Project**

- To build a scalable, modular data pipeline that automates the ingestion, transformation, and storage of sales and customer data.
- To enable the generation of insights such as top-performing salespeople, customer purchase trends, and monthly sales performance.
- To demonstrate core **Data Engineering** concepts like ETL (Extract, Transform, Load), data validation, data partitioning, and window functions.

---

## **Key Achievements**

1. Automated the ingestion of raw files from AWS S3 and their transformation into structured datasets.
2. Built data marts for customers and sales teams for business analysis and reporting.
3. Implemented dynamic ranking and incentive calculation for sales performance.
4. Used advanced data engineering techniques like window functions, partitioning, and cloud integrations.
5. Established end-to-end logging and monitoring to ensure traceability.
6. Organized data in S3 buckets for raw and processed stages, aligning with modern **Data Lake** principles.

---

## **Project Modules**

### **1. Data Ingestion**
- **Description**: Fetches raw files from S3 buckets and stores them locally for processing.
- **Technologies**: 
  - AWS S3 (via Boto3)
  - Python file handling
- **Tasks**:
  - Validating file names and formats.
  - Logging invalid files for error tracking.

---

### **2. Data Transformation**
#### a) **Customer Data Mart**
- **Objective**: Summarize customer purchase data to provide insights on spending trends.
- **Key Transformations**:
  - Aggregation of total purchases and expenditures by customer.
  - Addition of metadata for tracking updates.
- **Output**: Cleaned and aggregated data written into a **MySQL table**.

#### b) **Sales Team Data Mart**
- **Objective**: Evaluate monthly sales performance and calculate incentives.
- **Key Transformations**:
  - Calculated total monthly sales per salesperson using **window functions**.
  - Ranked salespeople within stores to identify top performers.
  - Incentive calculation for the best performer (1% of monthly sales).
  - Rounded financial values for accuracy.
- **Output**: Structured data written into another **MySQL table**.

---

### **3. Data Partitioning**
- **Description**: Partitioned the Sales Team Data Mart by store and month for improved query performance.
- **Technology**: PySpark write API
- **Output**: Partitioned files stored in AWS S3 under the processed directory.

---

### **4. Data Validation and Status Updates**
- **Description**: Ensures the integrity of processed data by updating file statuses in a MySQL staging table.
- **Technology**: MySQL
- **Tasks**:
  - Updating file statuses to 'Processed'.
  - Logging failed file updates for debugging.

---

### **5. Cleanup and Archival**
- **Description**: Maintains efficient storage by moving processed files to the S3 `processed` directory and deleting temporary local files.
- **Technology**:
  - AWS S3
  - Python file handling
- **Tasks**:
  - Organized raw and processed data in S3 buckets.
  - Removed temporary files from local storage after processing.

---

## **Detailed Data Pipeline Workflow**

1. **Ingestion**:
   - Raw sales and customer data files are fetched from the S3 bucket and validated locally.
   - Invalid files are logged for error reporting.

2. **Transformation**:
   - Using **PySpark**, the raw data is transformed:
     - **Customer Data Mart**: Aggregates customer-level purchase data.
     - **Sales Team Data Mart**: Summarizes monthly sales data, ranks salespeople, and calculates incentives.
   - Datasets are partitioned and written to MySQL tables and S3.

3. **Validation**:
   - A MySQL staging table tracks the status of processed files.
   - Files marked as successfully processed are logged as 'Processed.'

4. **Archival**:
   - Processed files are moved from the `raw` directory to the `processed` directory in S3.
   - Temporary files are deleted from local storage to maintain resource efficiency.

---

## **Data Engineering Concepts Used**

1. **ETL (Extract, Transform, Load)**:
   - Data is fetched from S3, transformed using PySpark, and loaded into MySQL and S3.

2. **Data Validation**:
   - Ensured only valid files were processed by checking file names and formats.

3. **Window Functions**:
   - Used for ranking salespeople and calculating monthly aggregates.

4. **Data Partitioning**:
   - Partitioned datasets by store and month for improved query performance.

5. **Cloud Integration**:
   - Used AWS S3 for scalable storage of raw and processed data.

6. **Database Interaction**:
   - MySQL tables were used for storing and tracking structured datasets.

7. **Data Lake Organization**:
   - Organized S3 directories into `raw` and `processed` buckets for a structured data lake.

8. **Logging and Monitoring**:
   - Implemented detailed logging for traceability of file ingestion and processing steps.

---

## **Architecture Diagram**

_(Add your architecture diagram here once it’s ready.)_

---

## **Setup Instructions**

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/sales-data-pipeline.git
   cd sales-data-pipeline
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure the project:
   - Add your AWS credentials and MySQL connection details in the `config.py` file.

4. Run the pipeline:
   ```bash
   python main.py
   ```

---

## **Technologies Used**

- **Programming Language**: Python
- **Big Data Framework**: Apache Spark (PySpark)
- **Cloud**: AWS S3
- **Database**: MySQL
- **Other Libraries**: Boto3, JDBC, Python logging
