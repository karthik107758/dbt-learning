## Snowflake

snowflake:
  type: snowflake
  account: <account>
  user: <user>
  password: <password>
  role: <role>
  database: <db>
  warehouse: <wh>
  schema: <schema>

## Databricks
databricks:
  type: databricks
  schema: <schema>
  host: <workspace-url>
  http_path: <http-path>
  token: <access-token>

## Airflow
DbtRunOperator(
    task_id='dbt_run',
    dir='/dbt',
    profiles_dir='/dbt/profiles',
    models='marts'
)

## Github Actions
- name: Run dbt
  run: dbt run --profiles-dir ./profiles
