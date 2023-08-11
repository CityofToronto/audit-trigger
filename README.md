# PostgreSQL Audit Triggers

We have tables that might change regularly. We want to automate storing the
changes to these tables, hence an audit table and an audit trigger. Based on
[Audit_trigger_91plus](http://wiki.postgresql.org/wiki/Audit_trigger_91plus)
with some improvements from
[pg-audit-trigger](https://github.com/circlehddev/pg-audit-trigger).

## How to use it

We currently have this set up in the `gis`, `collisions_replicator`, `wys`, `traffic`, and `miovision_api` schemas. To see which tables are
being logged `SELECT * FROM gis.audited_tables_list` or change the `gis` schema to the relevant one. To implement in a
new schema pop [`audit.sql`](audit.sql) in a query window and replace all `gis` with your schema.

To start logging a table run `SELECT gis.audit_table('gis.table_name')`.

Any change to a tables' rows (`INSERT, DELETE, UPDATE, TRUNCATE`) will be
stored in `gis.logged_actions`, including the timestamp of the action, the
action, and the data stored before the operation.
