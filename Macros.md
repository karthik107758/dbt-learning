{% macro clean_column(col_name) %}
  TRIM(LOWER({{ col_name }}))
{% endmacro %}

## Usage:

SELECT {{ clean_column('email') }} AS cleaned_email
FROM {{ ref('users') }}
