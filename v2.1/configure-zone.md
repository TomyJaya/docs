---
title: CONFIGURE ZONE
summary: Use the CONFIGURE ZONE statement to add, modify, reset, and remove replication zones.
toc: true
---

<span class="version-tag">New in v2.1:</span> Use `CONFIGURE ZONE` to add, modify, reset, and remove [replication zones](configure-replication-zones.html).

In CockroachDB, you can use **replication zones** to control the number and location of replicas for specific sets of data, both when replicas are first added and when they are rebalanced to maintain cluster equilibrium.

## Synopsis

<div>
  {% include {{ page.version.version }}/sql/diagrams/alter_zone_database.html %}
</div>

<div>
  {% include {{ page.version.version }}/sql/diagrams/alter_zone_index.html %}
</div>

<div>
  {% include {{ page.version.version }}/sql/diagrams/alter_zone_range.html %}
</div>

<div>
  {% include {{ page.version.version }}/sql/diagrams/alter_zone_table.html %}
</div>


## Required privileges

Currently, only the `root` user can configure replication zones.

## Parameters

 Parameter | Description
-----------+-------------
`name` | The name of the database, table, index, or range with the zone configuration you want to change.
`var_name` | The name of the constraint you want to change. For more information, see
`var_value` | The value of the constraint you want to change. For more information, see
`DISCARD` | Remove a zone configuration.
`DEFAULT` | Resets a zone configuration to inherited defaults.

### Variables





## Examples

### Edit a zone configuration

{% include copy-clipboard.html %}
~~~ sql
>
~~~

~~~

~~~

### Edit a zone configuration with compact constraint syntax


### Reset a zone configuration

### Remove a zone configuration


## See also

- [Configure Replication Zones](configure-replication-zones.html)
- [`ALTER DATABASE`](alter-database.html)
- [`ALTER TABLE`](alter-table.html)
- [`ALTER INDEX`](alter-index.html)
- [`ALTER RANGE`](alter-range.html)
- [Table Partitioning](partitioning.html)
- [Other SQL Statements](sql-statements.html)
