# Spotify End-To-End Data Engineering Project

## Introduction

This project aims to build an end-to-end data engineering pipeline that extracts, transforms, and loads (ETL) data using the Spotify API on AWS. The pipeline retrieves data from the Spotify API, transforms it into a desired format, and loads it into AWS data services for analysis.

## Table of Contents

- [Architecture Diagram](#architecture-diagram)
- [Tools and Technologies Used](#tools-and-technologies-used)
- [Project Workflow](#project-workflow)
- [Data Sources](#data-sources)
- [Methods](#methods)
- [Getting Started](#getting-started)
- [Contributing](#contributing)
- [License](#license)

## Architecture Diagram

![Architecture Diagram](https://drive.google.com/file/d/1kDP_ujM_vp_rxEL9VV0PKuRIR85o09hx/view?usp=sharing/architecture.drawio)


## Tools and Technologies Used

- **Programming Language**: Python
- **APIs**: [Spotify Web API](https://developer.spotify.com/documentation/web-api/)
- **Cloud Services**:
  - **AWS Lambda**: Serverless compute service for running code.
  - **AWS S3**: Storage service for raw and transformed data files.
  - **AWS CloudWatch**: Monitoring and management service for setting up triggers.
  - **AWS Glue**: ETL service for cataloging data.
  - **Amazon Athena**: Interactive query service for analyzing data using standard SQL.
- **Others**:
  - **AWS IAM**: For managing permissions.
  - **AWS SDK for Python (Boto3)**: For interacting with AWS services.
  - **Git & GitHub**: Version control and collaboration.

## Project Workflow

1. **Data Extraction**:
   - An AWS Lambda function is deployed to extract data from the Spotify API.
   - The function retrieves information such as playlists, tracks, and artists.
   - Extracted data is stored as JSON files in an AWS S3 bucket.

2. **Automated Trigger for Extraction**:
   - AWS CloudWatch Events are configured to trigger the Lambda extraction function automatically (e.g., daily at midnight).

3. **Data Transformation**:
   - A separate AWS Lambda function is created to transform the raw data.
   - The function processes the JSON files from S3, cleans the data, and structures it into a tabular format (e.g., CSV or Parquet).
   - Transformed data is saved back into a different folder within the S3 bucket.

4. **Automated Trigger for Transformation**:
   - Another CloudWatch Event or S3 event notification triggers the transformation Lambda function whenever new raw data is added.

5. **Data Storage in S3**:
   - Proper folder structures are maintained in S3 for raw and transformed data.
   - Example:
     - `s3://your-bucket/raw-data/`
     - `s3://your-bucket/transformed-data/`

6. **Data Cataloging with AWS Glue**:
   - AWS Glue Crawlers are set up to scan the transformed data in S3.
   - The crawler updates the AWS Glue Data Catalog with the latest schema.

7. **Data Analysis with Amazon Athena**:
   - Athena is used to run SQL queries on the cataloged data.
   - This enables quick and cost-effective data analysis without setting up a database.

## Data Sources

- **Spotify Web API**:
  - Documentation: [Spotify API Docs](https://developer.spotify.com/documentation/web-api/)
  - Provides access to Spotify's music data, including tracks, artists, albums, and playlists.


