# Docker-compose for MySQL
This docker-compose file is for spinning up MySQL server with utf8mb4, Japanese conscious character set.

# Precondition 
- Docker installed
- Docker compose installed
  
# Usage
1. Clone this repo
2. Run `docker-compose up --build`
3. Check if the tables are created as utf8mb4. Client also need to be switched to utf8mb4 to display data correctly. 

    In the case of Sequel Pro, Navigate to `Database -> Display with a specific Encode` and chose `utf8mb4` in the menu.
1. In the `portal-ext.properties`, set as follows.
   
   For 7.3, it's as follows.
   ```
    jdbc.default.driverClassName=com.mysql.cj.jdbc.Driver
    jdbc.default.url=jdbc:mysql://localhost/<YOUR DATABASE NAME>?connectionCollation=utf8mb4_bin&dontTrackOpenResources=true&holdResultsOpenOverStatementClose=true&serverTimezone=GMT&useFastDateParsing=false&useUnicode=true&characterEncoding=utf8
    jdbc.default.username=<YOUR USER NAME FOR DB>
    jdbc.default.password=<YOUR PASSWORD FOR DB>
   ```

# How to set up the default tables
Please see `db/mysql_init/01-databases.sql` and add tables accordingly.

# How to cleanup the environment.
1. Delete `db/mysql_data`
2. Run `docker-compose down --rmi all --volumes --remove-orphans`

# Appendix
## characterEncoding setting
As [the official document](https://dev.mysql.com/doc/connector-j/8.0/en/connector-j-reference-charsets.html) shows, 
```
For 8.0.12 and earlier: utf8
For 8.0.13 and later: utf8mb4
```
Please be careful in case you need to switch the MySQL image higher than Ver 8.