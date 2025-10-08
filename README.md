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

## 🧾 YAML Configurations

### `dbt_project.yml`

```yaml
name: my_dbt_project
version: '1.0'
profile: my_profile

models:
  my_dbt_project:
    staging:
      materialized: view
    marts:
      materialized: table

##sources.yml
version: 2
sources:
  - name: stripe
    schema: stripe_data
    tables:
      - name: payments
        columns:
          - name: id
            tests: [unique, not_null]
