def model(dbt, session):
    dbt.config(materialized="table")
    df = session.read_table("raw.customers")
    df = df.filter(df["is_active"] == True)
    df = df.withColumn("full_name", df["first_name"] + " " + df["last_name"])
    return df
