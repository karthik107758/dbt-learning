
Command	 Description	Example
dbt init	Initialize a new dbt project	dbt init my_project
dbt run	Run models	dbt run --select orders
dbt test	Run tests	dbt test --select customers
dbt seed	Load CSV files	dbt seed
dbt snapshot	Run snapshot logic	dbt snapshot
dbt compile	Compile models to SQL	dbt compile
dbt build	Run models, tests, seeds, snapshots	dbt build
dbt docs generate	Generate documentation	dbt docs generate
dbt docs serve	Serve docs locally	dbt docs serve
dbt run-operation	Run a macro	dbt run-operation my_macro
dbt show	Preview SQL results	dbt show --select orders
dbt source freshness	Check freshness of sources	dbt source freshness
