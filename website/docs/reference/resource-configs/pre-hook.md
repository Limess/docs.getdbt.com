---
resource_types: [models, seeds]
datatype: sql-statement | [sql-statement]
---

<Alert type='warning'>
<h4>Heads up!</h4>
This is a work in progress document. While this configuration applies to multiple resource types, the documentation has only been written for seeds.

</Alert>

## Definition
A SQL statement to be run after a model is created / a seed is updated.

Pre-hooks can also call macros that return SQL statements.

## Examples
Pre-hooks work very similarly to post-hooks, check out the [post-hook](post-hook.md) docs for more examples.
