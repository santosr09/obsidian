[Baeldung example](https://www.baeldung.com/database-migrations-with-flyway)
[Flyway example](https://documentation.red-gate.com/flyway/quickstart-how-flyway-works/quickstart-guides/quickstart-maven)
## Required dependencies

```
        <plugin>  
          <groupId>org.flywaydb</groupId>  
          <artifactId>flyway-maven-plugin</artifactId>  
          <version>10.11.0</version>  
  
          <configuration>            <url>jdbc:postgresql://localhost:5432/test-flyway</url>  
            <user>postgres</user>  
          </configuration>  
<!--          <configuration>  
            <user>postgres</user>            <password>postgres</password>            <schemas>              <schema>test-flyway</schema>            </schemas>          </configuration>-->        </plugin>
            
```

#### configuration using external configuration file
using a .conf file
```
flyway.user=databaseUser
flyway.password=databasePassword
flyway.schemas=schemaName
...
```
The default configuration file name is **flyway.conf** and by default it loads configuration files from:
- installDir/conf/flyway.conf
- userhome/flyway.conf
- workingDir/flyway.conf
If we use any other name (e.g _customConfig.conf_) as the configuration file, then we have to specify this explicitly when invoking the Maven command:
```
$ mvn -Dflyway.configFiles=customConfig.conf
```

#### Configuring using Systems properties
```
$ mvn -Dflyway.user=databaseUser -Dflyway.password=databasePassword 
  -Dflyway.schemas=schemaName
```

### Configuration order of precedence
The following is an order of precedence when a configuration is specified in more than one way:

1. System properties
2. External configuration file
3. Maven properties
4. Plugin configuration

### Migration directory in a java project
Here is where the migration scripts should be placed:
`src/main/resources/db/migration`.
Example:
`src/main/resources/db/migration/V1__Create_person_table.sql

#### Executing mvn migration, examples

```
$ mvn clean flyway:migrate
 
$ mvn clean flyway:migrate -Dflyway.configFiles=myFlywayConfig.conf

```


### Example of required dependencies using PostgreSQL
```
<!-- https://mvnrepository.com/artifact/org.flywaydb/flyway-database-postgresql -->  
<!-- If not:  org.flywaydb.core.api.FlywayException: No database found to handle jdbc:postgresql://localhost:5432/test-flyway-->  
<dependency>  
  <groupId>org.flywaydb</groupId>  
  <artifactId>flyway-database-postgresql</artifactId>  
  <version>10.11.0</version>  
  <scope>runtime</scope>  
</dependency>  
  
<!-- https://mvnrepository.com/artifact/org.postgresql/postgresql -->  
<!-- If not: org.flywaydb.core.api.FlywayException: Unable to instantiate JDBC driver: org.postgresql.Driver => Check whether the jar file is present-->  
    <dependency>  
      <groupId>org.postgresql</groupId>  
      <artifactId>postgresql</artifactId>  
      <version>42.7.3</version>  
    </dependency>
```