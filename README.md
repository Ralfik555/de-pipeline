# de-pipeline

End-to-end batch data pipeline built as a portfolio project: ingestion from a
public API, storage as Parquet, transformation with dbt, orchestration with
Airflow, processing with Spark, deployment to the cloud. Built step by step,
each step merged through a pull request.

## Goal

Show a complete data engineering workflow on one project, the way a small
production team would run it: versioned code, tests and linting on every PR,
containerised services, idempotent and schedulable jobs, and a documented data
model. The dataset is secondary; the engineering around it is the point.

## Planned architecture

Data flows in batches through the following stages:

1. **Ingestion**: a Python package pulls data from a public REST API with
   retries and logging, and writes raw records as Parquet files (bronze layer).
2. **Transformation**: dbt models build staging, intermediate and mart tables
   on top of the raw files, with schema and data tests.
3. **Orchestration**: Airflow runs ingestion and dbt as one scheduled DAG, with
   retries, backfill support and data quality checks.
4. **Processing at scale**: Spark on Databricks handles a larger public dataset,
   stored as partitioned Delta tables (bronze, silver, gold).
5. **Cloud**: the pipeline runs on AWS (S3 for storage, Glue Data Catalog and
   Athena for querying, scheduled ingestion with EventBridge and Lambda).

An architecture diagram will be added once the first three stages exist.

Open decisions:
- Data source for ingestion (decided in the next step).
- dbt engine: DuckDB or BigQuery sandbox.
- Cloud provider: AWS planned, GCP under consideration.

## Stack

| Layer           | Tools                                   |
|-----------------|-----------------------------------------|
| Language        | Python 3.12, pandas                     |
| Code quality    | pytest, ruff, GitHub Actions            |
| Storage formats | Parquet, Delta Lake                     |
| Transformation  | dbt, DuckDB                             |
| Orchestration   | Airflow (Docker Compose)                |
| Processing      | Spark on Databricks                     |
| Cloud           | AWS: S3, Glue, Athena, EventBridge, Lambda |
| Containers      | Docker                                  |

## Status

Last updated: 2026-11-11

- [x] Repository set up, `main` protected, changes via pull requests
- [ ] Data source chosen
- [ ] Ingestion package with tests
- [ ] Docker image and CI
- [ ] Data model and dbt project
- [ ] Airflow DAG
- [ ] Spark processing on Databricks
- [ ] AWS deployment
- [ ] Architecture diagram and final write-up

## How to run

Nothing to run yet. Instructions will appear with the ingestion package.