---
resource_types: all
datatype: string | [string]
---
<Alert type='warning'>
<h4>Heads up!</h4>
This is a work in progress document.

</Alert>

## Definition
Apply a tag (or list of tags) to a resource (models, seeds).

Tags can be used to select resources when running the following commands:
- `dbt run`
- `dbt seed`

## Examples
### Seeds

<File name='dbt_project.yml'>

```yml
seeds:
  jaffle_shop:
    utm_mappings:
      tags: marketing
```

</File>

<File name='dbt_project.yml'>

```yml
seeds:
  jaffle_shop:
    utm_mappings:
      tags:
        - marketing
        - hourly
```

</File>
