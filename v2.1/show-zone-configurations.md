---
title: SHOW ZONE CONFIGURATIONS
summary: The SHOW ZONE CONFIGURATIONS statement
toc: true
---

<span class="version-tag">New in v2.1:</span> The `SHOW ZONE CONFIGURATIONS` [statement](sql-statements.html) lists details about [replication zones](configure-replication-zones).

## Synopsis

<div>
{% include {{ page.version.version }}/sql/diagrams/show_zone.html %}
</div>

## Required privileges

No [privileges](privileges.html) are required to list the replication zones.

## Parameters

Parameter | Description
----------|------------
`zone_name` | The name of the system range for which to show zone configurations.
`database_name` | The name of the database for which to show zone configurations.
`table_name` | The name of the table for which to show zone configurations.
`partition_name` | The name of the partition for which to show zone configurations.
`index_name` | The name of the index for which to show zone configurations.

## Examples


### Show tables in the current database


### Show tables in a different schema


### Show tables in a different database



## See also

- [Configure Replcation Zones](configure-replication-zones.html)
- [`CONFIGURE ZONE`](configure-zone.html)
- [`ALTER DATABASE`](alter-database.html)
- [`ALTER INDEX`](alter-index.html)
- [`ALTER RANGE`](alter-range.html)
- [`ALTER TABLE`](alter-table.html)
- [SQL Statements](sql-statements.html)
