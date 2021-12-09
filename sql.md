## Change Database Tables to InnoDB
_Run this SQL Query in PhpMyAdmin (changing_ `DatabaseName` _to the actual database name). It will output a list of commands to change MyISAM tables to InnoDB. Be sure that you show full texts so that each command is not truncated._

```
SET @DATABASE_NAME = 'DatabaseName';

SELECT CONCAT('ALTER TABLE `', table_name, '` ENGINE=InnoDB;') AS sql_statements
FROM information_schema.tables AS tb
WHERE table_schema = @DATABASE_NAME
AND `ENGINE` = 'MyISAM'
AND `TABLE_TYPE` = 'BASE TABLE'
ORDER BY table_name DESC;
```
