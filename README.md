# ELT Pipeline with DBT and Snowflake

## Overview

This project implements an **ELT pipeline** using **DBT** for data transformation and **Snowflake** as the data warehouse. The pipeline follows a structured data flow:

- **Data Ingestion**: Synthetic data is generated in Python and stored in **Amazon S3**.
- **Data Loading**: Data is transferred from S3 to a **Snowflake staging table**.
- **Transformation**: DBT applies **incremental models** for optimized processing.
- **Consumption**: Processed data is accessed via **Tableau** or other BI tools.

## Architecture

![architecture]()

```
Source → S3 → Snowflake (Staging) → DBT (Transform) → Snowflake (Final) → BI Tool
```

## Technologies

- **Python** (`pandas`, `boto3`, `Faker`) – Data ingestion
- **Amazon S3** – Cloud storage
- **Snowflake** – Data warehouse
- **DBT** – Data transformation
- **Tableau** – Visualization

## Installation

```sh
python -m venv env
source env/bin/activate  # Windows: env\Scripts\activate
pip install -r requirements.txt
```

## Setup

1. Configure Snowflake in `profiles.yml`.
2. Generate data:
   ```sh
   python generate_data.py
   ```
3. Load data to Snowflake:
   ```sh
   python load_to_snowflake.py
   ```
4. Run DBT transformations:
   ```sh
   dbt run
   ```

## Incremental Processing

DBT processes only new or updated records:

```sh
dbt run --select incremental_orders
```

## Project Structure

```
📂 dbt_project       # DBT models
📂 scripts           # Python ingestion scripts
📂 config            # Configurations
generate_data.py     # Data generator
load_to_snowflake.py # Loads S3 to Snowflake
README.md            # Documentation
```

## Visualization

The transformed data is directly accessible in **Tableau** or other BI tools via Snowflake.

---

**Suggested Repository Name:** `elt-pipeline-dbt-snowflake`  
**Short Description:** "An end-to-end ELT pipeline using DBT, Snowflake, and S3 with incremental data processing."
