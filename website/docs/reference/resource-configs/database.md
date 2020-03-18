---
resource_types: [models, seeds]
datatype: string
---

<Alert type='warning'>
<h4>Heads up!</h4>
This is a work in progress document. While this configuration applies to multiple resource types, the documentation has only been written for seeds.

</Alert>

## Definition

Optionally specify a custom database for a [model](docs/docs/building-a-dbt-project/building-models.md) or [seed](docs/docs/building-a-dbt-project/seeds.md).

When dbt creates a relation (table/view) in a database, it creates it as: `{{ database }}.{{ schema }}.{{ identifier }}`, e.g. `analytics.finance.payments`

The standard behavior of dbt is:
* If a custom database is _not_ specified, the database of the relation is the target database (`{{ target.database }}`).
* If a custom database is specified, the database of the relation is the `{{ database }}` value.

To learn more about changing the way that dbt generates a relation's `database`, read [Using Custom Databases](docs/building-a-dbt-project/building-models/using-custom-database.md)

## Usage
### Load seeds into the RAW database
<File name='dbt_project.yml'>

```yml
seeds:
  database: RAW

```

</File>

## Warehouse specific information
* BigQuery: `project` and `database` are interchangeable
* Redshift: Cross-database queries are not possible in Redshift. As such, dbt will return a Database Error if you use this configuration.


## Changelog
* v0.16.0: Introduced in v0.16.0
