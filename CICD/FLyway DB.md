## Init
https://www.baeldung.com/database-migrations-with-flyway

### Migration types
Migrations can either be versioned or repeatable. 
- **versioned** : Has a unique version and is applied exactly once. 
- **repetable** : Doesn’t have a version. Instead, they are (re-)applied every time their checksum changes.

Within a single migration run, repeatable migrations are always applied last, after pending versioned migrations have been executed. Repeatable migrations are applied in order of their description. For a single migration, all statements are run within a single database transaction.

[Project example](https://dzone.com/articles/how-to-use-flyway-for-database-migration-in-spring)

