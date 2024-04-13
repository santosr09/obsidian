Flyway adheres to the following **naming convention for migration scripts:**

_\<Prefix>\<Version>__\<Description>.sql_

Where:

- _\<Prefix>_ – The default prefix is _V_, which we can change in the above configuration file using the _flyway.sqlMigrationPrefix_ property.
- _\<Version>_ – Migration version number. Major and minor versions may be separated by an _underscore_. **The migration version should always start with 1.**
- _\<Description>_ – Textual description of the migration. A double underscore separates the description from the version numbers.

Example: _V1_1_0__my_first_migration.sql_

[[Flyway using MVN plugin#Migration directory in a java project]]
