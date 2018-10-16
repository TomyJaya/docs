---
title: Experimental Features
summary: Learn about the experimental features available in CockroachDB v2.1
toc: true
---

This page lists the experimental features that are available in CockroachDB 2.1.

{{site.data.alerts.callout_danger}}
**This page describes experimental features.**  Their interfaces and outputs are subject to change, and there may be bugs.
<br />
If you encounter a bug, please [file an issue](file-an-issue.html).
{{site.data.alerts.end}}

## Session variables

The table below lists the experimental session variables for CockroachDB 2.1.  For a complete list of session variables, see [`SHOW` (session settings)](show-vars.html).

| Variable                            | Default Value | Description                                                                                                                                                                                                                                                                          |
|-------------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `experimental_force_lookup_join`    | `'off'`       | Indicates whether the planner should try and plan a lookup join where the left side is scanned and index lookups are done on the right side. Will emit a warning if a lookup join can't be planned.                                                                                  |
| `experimental_force_split_at`       | `'off'`       | Indicates whether checks to prevent incorrect usage of `ALTER TABLE ... SPLIT AT` should be skipped.                                                                                                                                                                                 |
| `experimental_force_zigzag_join`    | `'off'`       | If `'on'`, the planner will try and plan a zigzag join. Will emit a warning if a zigzag join can't be planned.                                                                                                                                                                       |
| `experimental_serial_normalization` | `'rowid'`     | If set to `'virtual_sequence'`, make the [`SERIAL`](serial.html) pseudo-type optionally auto-create a sequence for [better compatibility with Hibernate sequences](https://forum.cockroachlabs.com/t/hibernate-sequence-generator-returns-negative-number-and-ignore-unique-rowid/). |

## SQL statements

### Keep SQL audit logs

Log queries against a table to a file. For more information, see [`ALTER TABLE ... EXPERIMENTAL_AUDIT`](experimental-audit.html).

{% include copy-clipboard.html %}
~~~ sql
> ALTER TABLE t EXPERIMENTAL_AUDIT SET READ WRITE;
~~~

### Relocate leases

Distributes ranges across nodes.  The example below distributes ranges for the primary index across the first 3 nodes in the cluster.

{% include copy-clipboard.html %}
~~~ sql
> ALTER TABLE t EXPERIMENTAL_RELOCATE SELECT ARRAY[i], i FROM generate_series(1,3) AS g(i);
~~~

### Show statement fingerprints

If two expressions share the same fingerprint, then they are the identical expression.  Fingerprints are used by the [cost-based optimizer](cost-based-optimizer.html) for plan caching.

Example:

{% include copy-clipboard.html %}
~~~ sql
> SHOW EXPERIMENTAL_FINGERPRINTS FROM TABLE t;
~~~

### Show a table's ranges

Show the ranges that make up a table or index.  For more information, see [`SHOW EXPERIMENTAL_RANGES`](show-experimental-ranges.html).

{% include copy-clipboard.html %}
~~~ sql
SHOW EXPERIMENTAL_RANGES FROM TABLE t;
~~~

### Turn on KV event tracing

Use session tracing (via [`SHOW TRACE`](show-trace.html)) to report the replicas of all KV events that occur during its execution.

Example:

XXX: FIND A GOOD QUERY

{% include copy-clipboard.html %}
~~~ sql
> SHOW EXPERIMENTAL_REPLICA TRACE FOR ...;
~~~

### Check for constraint violations with `SCRUB`

Checks the consistency of `UNIQUE` indexes, `CHECK CONSISTENCY` constraints, and other constraints.  Partially implemented; see [cockroachdb/cockroach#10425](https://github.com/cockroachdb/cockroach/issues/10425) for details.

XXX: FIND A REAL QUERY

{% include copy-clipboard.html %}
~~~ sql
> EXPERIMENTAL SCRUB {TABLE,DATABASE} ...;
~~~

### OLD TABLE

The table below lists the experimental SQL statements available in CockroachDB 2.1, with usage examples and brief descriptions of each.

| Feature                | Example SQL Statement                                                                      | Description                                                                                                                                                                                                                       |
|------------------------+--------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SQL audit logs         | `ALTER TABLE t EXPERIMENTAL_AUDIT SET READ WRITE`                                          | Log queries against a table to a file. For more information, see [`ALTER TABLE ... EXPERIMENTAL_AUDIT`](experimental-audit.html).                                                                                                 |
| Lease relocation       | `ALTER TABLE t EXPERIMENTAL_RELOCATE SELECT ARRAY[i], i FROM generate_series(1,3) AS g(i)` | Distribute ranges across nodes.  The example distributes ranges for the primary index across the first 3 nodes in the cluster.                                                                                                    |
| Statement fingerprints | `SHOW EXPERIMENTAL_FINGERPRINTS FROM TABLE t`                                              | If two expressions share the same fingerprint, then they are the identical expression.  Fingerprints are used by the [cost-based optimizer](cost-based-optimizer.html) for plan caching.                                          |
| Show a table's ranges  | `SHOW EXPERIMENTAL_RANGES FROM TABLE t`                                                    | Show the ranges that make up a table or index.  For more information, see [`SHOW EXPERIMENTAL_RANGES`](show-experimental-ranges.html).                                                                                            |
| KV event tracing       | `SHOW EXPERIMENTAL_REPLICA TRACE FOR ...`                                                  | Use session tracing (via [`SHOW TRACE`](show-trace.html)) to report the replicas of all KV events that occur during its execution.                                                                                                |
| Constraint checker     | `EXPERIMENTAL SCRUB {TABLE,DATABASE} ...`                                                  | Checks the consistency of `UNIQUE` indexes, `CHECK CONSISTENCY` constraints, and other constraints.  Partially implemented; see [cockroachdb/cockroach#10425](https://github.com/cockroachdb/cockroach/issues/10425) for details. |

## Functions and Operators

The table below lists the experimental SQL functions and operators available in CockroachDB 2.1.  For more information, see each function's documentation at [Functions and Operators](functions-and-operators.html).

| Function                                                                         | Description                                     |
|----------------------------------------------------------------------------------+-------------------------------------------------|
| [`experimental_strftime`](functions-and-operators.html#date-and-time-functions)  | Format time using standard `strftime` notation. |
| [`experimental_strptime`](functions-and-operators.html#date-and-time-functions)  | Format time using standard `strptime` notation. |
| [`experimental_uuid_v4()`](functions-and-operators.html#id-generation-functions) | Return a UUID.                                  |

## See Also

- [`SHOW` (session)](show-vars.html)
- [Functions and Operators](functions-and-operators.html)
- [`ALTER TABLE ... EXPERIMENTAL_AUDIT`](experimental-audit.html)
- [`SHOW EXPERIMENTAL_RANGES`](show-experimental-ranges.html)
- [`SHOW TRACE`](show-trace.html)
