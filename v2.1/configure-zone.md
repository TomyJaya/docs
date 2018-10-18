---
title: CONFIGURE ZONE
summary: Use the CONFIGURE ZONE statement to add, modify, reset, and remove replication zones.
toc: true
---

<span class="version-tag">New in v2.1:</span> Use `CONFIGURE ZONE` to add, modify, reset, and remove [replication zones](configure-replication-zones.html).

In CockroachDB, you can use **replication zones** to control the number and location of replicas for specific sets of data, both when replicas are first added and when they are rebalanced to maintain cluster equilibrium.

## Synopsis

**alter_zone_range_stmt ::=**

<div>
  {% include {{ page.version.version }}/sql/diagrams/alter_zone_range.html %}
</div>

**alter_zone_database_stmt ::=**

<div>
  {% include {{ page.version.version }}/sql/diagrams/alter_zone_database.html %}
</div>

**alter_zone_table_stmt ::=**

<div>
  {% include {{ page.version.version }}/sql/diagrams/alter_zone_table.html %}
</div>

**alter_zone_index_stmt ::=**

<div>
  {% include {{ page.version.version }}/sql/diagrams/alter_zone_index.html %}
</div>

## Required privileges

Currently, only the `root` user can configure replication zones.

## Parameters

 Parameter | Description
-----------+-------------
`range_name` | The name of the system [range](architecture/overview.html#glossary) for which to show [replication zone configurations](configure-replication-zones).
`database_name` | The name of the [database](create-database.html) for which to show [replication zone configurations](configure-replication-zones).
`table_name` | The name of the [table](create-table.html) for which to show [replication zone configurations](configure-replication-zones).
`partition_name` | The name of the [partition](partitioning.html) for which to show [replication zone configurations](configure-replication-zones).
`index_name` | The name of the [index](indexes.html) for which to show [replication zone configurations](configure-replication-zones).
`variable` | The name of the [variable](#variables) to change.
`value` | The value of the variable to change.
`DISCARD` | Remove a zone configuration.

### Variables

{% include v2.1/zone-configs/variables.md %}

## Examples

### Edit a zone configuration

{% include copy-clipboard.html %}
~~~ sql
> ALTER TABLE t CONFIGURE ZONE USING range_min_bytes = 0, range_max_bytes = 90000, gc.ttlseconds = 89999, num_replicas = 4, constraints = '[-region=west]';
~~~

~~~
CONFIGURE ZONE 1
~~~


### Reset a zone configuration

{% include copy-clipboard.html %}
~~~ sql
> ALTER TABLE t CONFIGURE ZONE USING DEFAULT;
~~~

~~~
CONFIGURE ZONE 1
~~~

### Remove a zone configuration

{% include copy-clipboard.html %}
~~~ sql
> ALTER TABLE t CONFIGURE ZONE DISCARD;
~~~

~~~
CONFIGURE ZONE 1
~~~

## See also

- [Configure Replication Zones](configure-replication-zones.html)
- [`ALTER DATABASE`](alter-database.html)
- [`ALTER TABLE`](alter-table.html)
- [`ALTER INDEX`](alter-index.html)
- [`ALTER RANGE`](alter-range.html)
- [Table Partitioning](partitioning.html)
- [Other SQL Statements](sql-statements.html)
