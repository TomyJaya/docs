---
title: SHOW ZONE CONFIGURATIONS
summary: Use the SHOW ZONE CONFIGURATIONS statement to list details about existing replication zones.
toc: true
---

<span class="version-tag">New in v2.1:</span> Use the `SHOW ZONE CONFIGURATIONS` [statement](sql-statements.html) to list details about existing [replication zones](configure-replication-zones).

## Synopsis

<div>
{% include {{ page.version.version }}/sql/diagrams/show_zone.html %}
</div>

## Required privileges

No [privileges](privileges.html) are required to list replication zones.

## Parameters

Parameter | Description
----------|------------
`range_name` | The name of the system [range](architecture/overview.html#glossary) for which to show [replication zone configurations](configure-replication-zones).
`database_name` | The name of the [database](create-database.html) for which to show [replication zone configurations](configure-replication-zones).
`table_name` | The name of the [table](create-table.html) for which to show [replication zone configurations](configure-replication-zones).
`partition_name` | The name of the [partition](partitioning.html) for which to show [replication zone configurations](configure-replication-zones).
`index_name` | The name of the [index](indexes.html) for which to show [replication zone configurations](configure-replication-zones).

## Examples


### Show all zone configurations

{% include copy-clipboard.html %}
~~~ shell
> SHOW ALL ZONE CONFIGURATIONS;
~~~

~~~
      zone_name      |                         config_sql
+--------------------+------------------------------------------------------------+
  .default           | ALTER RANGE default CONFIGURE ZONE USING
                     |     range_min_bytes = 1048576,
                     |     range_max_bytes = 67108864,
                     |     gc.ttlseconds = 90000,
                     |     num_replicas = 3,
                     |     constraints = '[]',
                     |     lease_preferences = '[]'
  system             | ALTER DATABASE system CONFIGURE ZONE USING
                     |     range_min_bytes = 1048576,
                     |     range_max_bytes = 67108864,
                     |     gc.ttlseconds = 90000,
                     |     num_replicas = 5,
                     |     constraints = '[]',
                     |     lease_preferences = '[]'
  system.jobs        | ALTER TABLE system.public.jobs CONFIGURE ZONE USING
                     |     range_min_bytes = 1048576,
                     |     range_max_bytes = 67108864,
                     |     gc.ttlseconds = 600,
                     |     num_replicas = 5,
                     |     constraints = '[]',
                     |     lease_preferences = '[]'
  .meta              | ALTER RANGE meta CONFIGURE ZONE USING
                     |     range_min_bytes = 1048576,
                     |     range_max_bytes = 67108864,
                     |     gc.ttlseconds = 3600,
                     |     num_replicas = 5,
                     |     constraints = '[]',
                     |     lease_preferences = '[]'
  .system            | ALTER RANGE system CONFIGURE ZONE USING
                     |     range_min_bytes = 1048576,
                     |     range_max_bytes = 67108864,
                     |     gc.ttlseconds = 90000,
                     |     num_replicas = 5,
                     |     constraints = '[]',
                     |     lease_preferences = '[]'
  .liveness          | ALTER RANGE liveness CONFIGURE ZONE USING
                     |     range_min_bytes = 1048576,
                     |     range_max_bytes = 67108864,
                     |     gc.ttlseconds = 600,
                     |     num_replicas = 5,
                     |     constraints = '[]',
                     |     lease_preferences = '[]'
  tpch               | ALTER DATABASE tpch CONFIGURE ZONE USING
                     |     constraints = '[]'
  tpch.customer      | ALTER TABLE tpch.public.customer CONFIGURE ZONE USING
                     |     range_min_bytes = 40000
  zone_config_test.t | ALTER TABLE zone_config_test.public.t CONFIGURE ZONE USING
                     |     range_min_bytes = 0,
                     |     range_max_bytes = 90000,
                     |     gc.ttlseconds = 89999,
                     |     num_replicas = 4,
                     |     constraints = '[-region=west]'
(9 rows)
~~~

### Show zone configurations for a table

{% include copy-clipboard.html %}
~~~ shell
> SHOW ZONE CONFIGURATION FOR TABLE customer;
~~~
~~~
    zone_name   |                      config_sql
+---------------+-------------------------------------------------------+
  tpch.customer | ALTER TABLE tpch.public.customer CONFIGURE ZONE USING
                |     range_min_bytes = 40000,
                |     range_max_bytes = 67108864,
                |     gc.ttlseconds = 90000,
                |     num_replicas = 3,
                |     constraints = '[]',
                |     lease_preferences = '[]'
(1 row)
~~~


## See also

- [Configure Replication Zones](configure-replication-zones.html)
- [`CONFIGURE ZONE`](configure-zone.html)
- [`ALTER DATABASE`](alter-database.html)
- [`ALTER INDEX`](alter-index.html)
- [`ALTER RANGE`](alter-range.html)
- [`ALTER TABLE`](alter-table.html)
- [SQL Statements](sql-statements.html)
