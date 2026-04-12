# Reddit Data Engineering Pipeline

This project provides a comprehensive data pipeline solution to extract, transform, and load (ETL) Reddit data into an AWS-based data lake and warehouse. The pipeline leverages Apache Airflow for orchestration, Docker for containerization, and AWS services for storage.

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [System Setup](#system-setup)
- [Troubleshooting](#troubleshooting)

## Overview

The pipeline is designed to:

1. Extract data from Reddit using its API.
2. Store the raw data into an S3 bucket from Airflow.
3. Transform the data using AWS Glue and Amazon Athena.
4. Load the transformed data into Amazon Redshift for analytics and querying.

## Architecture
1. **Reddit API**: Source of the data.
2. **Apache Airflow & Celery**: Orchestrates the ETL process and manages task distribution.
3. **PostgreSQL**: Temporary storage and metadata management.
4. **Amazon S3**: Raw data storage.
5. **AWS Glue**: Data cataloging and ETL jobs.
6. **Amazon Athena**: SQL-based data transformation.
7. **Amazon Redshift**: Data warehousing and analytics.

## Prerequisites
- **AWS Account**: Permissions for S3, Glue, Athena, and Redshift.
- **Reddit API Credentials**: Create a "script" app at [reddit.com/prefs/apps](https://www.reddit.com/prefs/apps).
- **Docker Desktop**: Installed and running.
- **Python 3.9+**: For local script reference (optional).

## System Setup
1. Clone the repository.
   ```bash
   git clone https://github.com/Tarunvetsa/RedditDataEngineering.git
   ```
2. Rename the configuration file and the credentials to the file.
   ```bash
    mv config/config.conf.example config/config.conf
   ```
   Open config/config.conf and update your Reddit and AWS keys.

3. Build and Start Containers. Use Docker to handle all dependencies:
   ```powershell
    docker-compose up -d --build
   ```

4. Initialize Airflow Database.
   ```powershell
    docker-compose up airflow-init
   ```
Wait until the terminal shows this process has finished before moving to the next step.


5. Launch the Airflow web UI.
   ```bash
    open http://localhost:8080
   ```
   **Default Credentials**:
   - **Username**: `airflow`
   - **Password**: `airflow`



## Troubleshooting

### Localhost Refused to Connect
Airflow takes a few minutes to start up. If the site doesn't load immediately, wait 2 minutes. If it still fails:
* Run `docker ps` to ensure `airflow-webserver` is running.
* Check logs: `docker logs redditdataengineering-airflow-webserver-1`


### Stopping the Project
When you are finished working, use these commands to manage your environment:

* **To Pause**: Keeps the containers and data but stops execution to save RAM.
  ```powershell
  docker-compose stop