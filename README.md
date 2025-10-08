# dbt-learning
# 📘 dbt Project Guide

Welcome to the dbt (Data Build Tool) project! This guide provides a comprehensive overview of dbt concepts, configurations, syntax, and integrations to help you build scalable, testable, and well-documented data pipelines.

---

## 🧠 What Is dbt?

dbt enables analytics engineers to transform raw data in the warehouse using SQL while applying software engineering best practices like modularity, version control, testing, and documentation.

---

## 📦 Core Concepts

| Component   | Description |
|------------|-------------|
| **Model**   | SQL file that defines a transformation |
| **Seed**    | CSV file loaded into the warehouse |
| **Snapshot**| Tracks slowly changing dimensions |
| **Source**  | External table used in models |
| **Test**    | Validates data quality |
| **Macro**   | Reusable SQL logic using Jinja |
| **Documentation** | Auto-generated docs from your dbt project |

---
## Jinja Reference
{{ ref('model_name') }}         → Reference another model
{{ source('src', 'table') }}    → Reference external source
{{ config(materialized='table') }} → Set model config
{{ var('region') }}             → Use variable
{{ log('message', info=True) }} → Log messages

🧱 Materialization Options
Type	Description
view	Virtual table
table	Physical table
incremental	Append new data
ephemeral	CTE only

{{ config(materialized='incremental', unique_key='id') }}

SCD Types with snapshots
Type1(overwrite):
SELECT * FROM {{ source('crm', 'customers') }}

Type2:
{% snapshot customers_snapshot %}
  {{
    config(
      strategy='timestamp',
      updated_at='updated_at',
      unique_key='customer_id'
    )
  }}
  SELECT * FROM {{ source('crm', 'customers') }}
{% endsnapshot %}

Type3:
SELECT
  email AS current_email,
  LAG(email) OVER (...) AS previous_email
FROM {{ source('crm', 'customers') }}

Tests:
Test Type	Purpose
unique	Ensure no duplicates
not_null	Ensure required fields
relationships	Foreign key integrity
accepted_values	Enum-like constraints
