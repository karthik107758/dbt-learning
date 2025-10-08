## Syntax
{% macro macro_name(arg1, arg2) %}
  -- Your logic here
{% endmacro %}

## Call a macro
{{ macro_name('value1', 'value2') }}

## Example 1: Simple column cleaner

{% macro clean_column(col_name) %}
  TRIM(LOWER({{ col_name }}))
{% endmacro %}

## Usage:

SELECT {{ clean_column('email') }} AS cleaned_email
FROM {{ ref('users') }}

## Example 2: Dynamic Date Filter

{% macro filter_by_date(table, date_col, days_back=7) %}
  SELECT *
  FROM {{ table }}
  WHERE {{ date_col }} >= CURRENT_DATE - INTERVAL '{{ days_back }} days'
{% endmacro %}

## Usage:
{{ filter_by_date(ref('orders'), 'order_date', 30) }}

## Example3: Generate Surrogatekey
{% macro generate_surrogate_key(cols) %}
  MD5(CONCAT({{ cols | join(', ') }}))
{% endmacro %}

## Usage
SELECT {{ generate_surrogate_key(['customer_id', 'order_id']) }} AS sk
FROM {{ ref('orders') }}


📦 Built-in Macros (via dbt-utils)
If you install dbt-utils, you get access to powerful macros like:
get_column_values()
date_spine()
surrogate_key()
star()
generate_series()
Install via packages.yml:
packages:
  - package: dbt-labs/dbt_utils
    version: 1.1.1
Run bash command
dbt deps


