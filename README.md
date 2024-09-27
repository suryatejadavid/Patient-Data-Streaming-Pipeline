# Patient-Data-Streaming-Pipeline

## Overview

This project implements a real-time **Patient Data Pipeline** using Databricks' Delta Live Tables (DLT). The pipeline processes streaming healthcare data in three layers: **Bronze**, **Silver**, and **Gold**. The goal is to ingest, transform, clean, and aggregate patient records for analytics and reporting, enabling near real-time insights into patient health data.

## Pipeline Layers

1. **Bronze Layer:**
   - Raw data is ingested every 2 minutes from various patient data sources.
   - The data remains in its original form with minimal transformations (e.g., schema enforcement, null handling).
   - Data is stored in Delta Lake tables for further processing.

2. **Silver Layer:**
   - Data cleaning and transformations are applied.
   - Data from the Bronze layer is joined with external reference data (e.g., diagnosis mapping).
   - Duplicate records, inconsistencies, and missing values are addressed to produce a clean, standardized dataset.

3. **Gold Layer:**
   - Final aggregation, windowing, and data quality checks are performed.
   - The Gold layer provides rich, refined data, optimized for analytics, such as average patient metrics, diagnosis-specific summaries, and time-series trends.
   - Data quality checks ensure that records meet the required criteria.

## Features

- **Real-time data ingestion:** Synthetic healthcare data is generated every 2 minutes and ingested into Databricks using the Autoloader or Spark Streaming.
- **Delta Live Tables (DLT):** Automatically handles the transformation and data quality checks as the data flows from the Bronze to the Gold layer.
- **Data quality checks:** Ensure the integrity of the data before it reaches the final analytical layer.
- **Aggregations and windowing:** Perform advanced calculations like rolling averages and real-time patient monitoring.

## Setup and Installation

1. **Databricks Environment:**
   - Ensure you have access to a Databricks workspace with Delta Live Tables enabled. I am using Databricks hosted on AWS
   - Clone this repository and upload the necessary files to your Databricks workspace.

2. **Data Ingestion:**
   - Use the Python script `data_generator.py` or any source that can stream the data to generate synthetic patient data every 2 minutes. This data is saved as CSV files or streamed directly to the Bronze table.
   - Example command:
     ```bash
     python data_generator.py
     ```

3. **Delta Live Tables Configuration:**
   - Set up the DLT pipeline in Databricks by creating a new DLT notebook. Follow the steps outlined in the `dlt_pipeline_notebook.sql` file for the transformations and quality checks.
   - Define the Bronze, Silver, and Gold tables in your DLT pipeline.

4. **Automating the Process:**
   - Use Databricks Jobs to schedule the DLT pipeline for continuous transformation of data.
   - Configure Databricks Autoloader to detect new files and ingest them automatically into the Bronze layer.

## Data Structure

### Files

- **patients_daily_file_*.csv:**
  - Contains synthetic daily records of patients, including patient information such as ID, name, age, gender, admission date, and diagnosis code.
  
- **diagnosis_mapping.csv:**
  - Contains mappings of diagnosis codes to human-readable diagnosis descriptions.

### Table Definitions

- **Bronze Table:**
  - Raw data as ingested from the CSV files.
  
- **Silver Table:**
  - Cleaned and transformed data with all inconsistencies and missing values addressed.
  
- **Gold Table:**
  - Aggregated, windowed, and validated data, optimized for analytics and reporting.

## Future Enhancements

- Implement a more complex data generation mechanism for simulating different healthcare scenarios.
- Add more advanced machine learning models for real-time patient risk prediction based on ingested data.
- Implement dashboarding for live monitoring and alerts.

