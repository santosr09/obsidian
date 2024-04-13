
[Baeldung](https://www.baeldung.com/database-migrations-with-flyway)
[quickstart-how-flyway-works](https://documentation.red-gate.com/flyway/quickstart-how-flyway-works)

To keep track of which migrations we’ve already applied and when, it adds a special bookkeeping table to our schema. This **metadata table** also tracks **migration checksums**, and whether or not the migrations were successful.

The framework performs the following steps to accommodate evolving database schemas:

1. It checks a database schema to locate its metadata table (_SCHEMA_VERSION_ by default). If the metadata table doesn’t exist, it will create one.
2. It scans an application classpath for available migrations.
3. It compares migrations against the metadata table. If a version number is lower or equal to a version marked as current, it’s ignored.
4. It marks any remaining migrations as pending migrations. These are sorted based on the version number and are executed in order.
5. As each migration is applied, the metadata table is updated accordingly.