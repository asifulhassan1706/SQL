# SQL Database Administrator – Essential Queries & Commands
This file lists the most common SQL queries and administrative commands used by Database Administrators (DBAs) with a short description of what each does.
## 📝 1. Database Information
```sql
# Show all databases in the server
SHOW DATABASES;

# Show current database
SELECT DATABASE();

# Create a DATABASE
CREATE DATABASE <DATABASENAME>;
USE <DATABASENAME>;

# Show all tables in current database
SHOW TABLES;

# Describe table structure (columns, types)
DESCRIBE table_name;
````

## 📝 2. User & Permission Management

```sql
# Create a new user
CREATE USER 'username'@'host' IDENTIFIED BY 'password';

# Grant privileges on a database
GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'host';

#Show current user privileges
SHOW GRANTS FOR 'username'@'host';

#Revoke privileges
REVOKE ALL PRIVILEGES ON database_name.* FROM 'username'@'host';

#Change user password
ALTER USER 'username'@'host' IDENTIFIED BY 'newpassword';
```

## 📝 3. Backup & Restore(MySQL terminal)

```sql
#(MySQL) Export database (from terminal)
mysqldump -u user -p database_name > backup.sql

#(MySQL) Import database
mysql -u user -p database_name < backup.sql

#(SQL Server) Backup a database
BACKUP DATABASE database_name TO DISK = 'C:\backup.bak';

#(SQL Server) Restore a database
RESTORE DATABASE database_name FROM DISK = 'C:\backup.bak' WITH REPLACE;
```

## 📝 4. Performance & Monitoring

```sql
#Show currently running queries (MySQL)
SHOW PROCESSLIST;

#Show database size per table (MySQL)
SELECT table_schema AS `Database`, 
       SUM(data_length + index_length) / 1024 / 1024 AS `Size (MB)`
FROM information_schema.TABLES
GROUP BY table_schema;

#Check query execution plan
EXPLAIN SELECT * FROM table_name WHERE condition;
```

## 📝 5. Maintenance Tasks

```sql
#Optimize table to reclaim space
OPTIMIZE TABLE table_name;

#Analyze table to update statistics
ANALYZE TABLE table_name;

#Check table for errors
CHECK TABLE table_name;
```

---

## 📝 6. Creation,Changing and Deletion

```sql
#Create a new table

CREATE TABLE employees (
  id INT PRIMARY KEY AUTO_INCREMENT,
  first_name VARCHAR(50),
  last_name VARCHAR(50)
);

#Delete table
DROP TABLE employees;

#Delete The Column
ALTER TABLE <TABLENAME> DROP COLUMN <COLUMNNAME>;

#Delete Data From Column
DELETE FROM <TABLENAME> WHERE <COLUMNNAME><80;

#Erase ALL Data From Table
TRUNCATE TABLE <TABLENAME>;

#Adding The Column
ALTER TABLE <TABLENAME> ADD COLUMN designation VARCHAR(100);

#Rename The Table
ALTER TABLE <TABLENAME> RENAME TO <TABLENAME>;

#Change The Column
ALTER TABLE <TABLENAME> CHANGE COLUMN ID DEPT_ID INT PRIMARY KEY;

#Modify The Column
ALTER TABLE <TABLENAME> MODIFY <COLUMNNAME> DATATYPE NOT NULL;
```

## 📝 7. AGGREGATE FUNCTION
```sql
#Maximum Value OF a Column
SELECT MAX(COLUMNNAME) FROM <TABLENAME> GROUP BY <COLUMNNAME>;

#Count The Column Value each
SELECT CITY,COUNT(COLUMNNAME) FROM <TABLENAME> GROUP BY <CLOUMNNAME>;

#Minimum Value Of a Column
SELECT CITY,MIN(COLUMNNAME) FROM <TABLENAME> GROUP BY <CLOUMNNAME>;

#SUM Of Column Value
SELECT CITY,SUM(COLUMNNAME) FROM <TABLENAME> GROUP BY <CLOUMNNAME>;

#Average Of Column Value
SELECT CITY,AVG(COLUMNNAME) FROM <TABLENAME> GROUP BY <CLOUMNNAME>;
```

## 📝 8. Common DML (Data Manipulation Language)

```sql
#Insert data
INSERT INTO employees (first_name, last_name, designation)
VALUES('John', 'Doe', 'Manager');

#Update data
UPDATE employees SET designation = 'Team Lead' WHERE id = 1;

#Delete data
DELETE FROM employees WHERE id = 1;

#Select with conditions
SELECT * FROM employees WHERE designation = 'Manager';
```

## 📝 9. Joins & Views

* **INNER JOIN Two tables**
```sql
SELECT e.id, e.first_name, e.last_name, d.designation
FROM employees e
JOIN designations d 
ON e.designation_id = d.id;
```
```sql
SELECT * FROM STUDENT 
INNER JOIN COURSE 
ON STUDENT.STUDENT_ID=COURSE.STUDENT_ID;
```
* **LEFT JOIN**
```sql
SELECT * FROM STUDENT AS S 
LEFT JOIN COURSE AS C 
ON S.STUDENT_ID=C.STUDENT_ID;
```
* **RIGHT JOIN**
```sql
SELECT * FROM STUDENT AS S 
LEFT JOIN COURSE AS C 
ON S.STUDENT_ID=C.STUDENT_ID;
```

* **FULL JOIN**
```sql
SELECT * FROM STUDENT AS S 
LEFT JOIN COURSE AS C 
ON S.STUDENT_ID=C.STUDENT_ID
UNION
SELECT * FROM STUDENT AS S 
LEFT JOIN COURSE AS C 
ON S.STUDENT_ID=C.STUDENT_ID;
```

* **SELF JOIN**
```sql
SELECT * FROM STUDENT AS S 
JOIN COURSE AS C 
ON S.STUDENT_ID=C.STUDENT_ID;
```
* **UNION(For Unique Value)**
```sql
SELECT <CLOUMNNAME> FROM STUDENT
UNION
SELECT NAME FROM STUDENT;
```

* **UNION ALL(For All Value)**
```sql
SELECT <CLOUMNNAME> FROM STUDENT
UNION ALL
SELECT NAME FROM STUDENT;
```

* **Create a View for Repeated Query**
```sql
CREATE VIEW active_employees AS
SELECT * FROM employees WHERE status = 'Active';
```
```sql
CREATE VIEW VIEW1 AS
SELECT rollno,name,marks FROM student;
```

* **Query the View**
```sql
SELECT * FROM active_employees;
```
```sql
SELECT * FROM VIEW1;
```
```sql
DROP VIEW VIEW1; #Delete Table
```
## 📝 9. Transactions

```sql
#Start transaction
START TRANSACTION;

#Do multiple operations
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

#Commit changes
COMMIT;

#Or rollback if something went wrong
ROLLBACK;
```

## 📝 10. Indexing & Constraints

```sql
#Create index
CREATE INDEX idx_lastname ON employees(last_name);

#Drop index (MySQL)
DROP INDEX idx_lastname ON employees;

#Add foreign key

ALTER TABLE employees 
ADD CONSTRAINT fk_designation 
FOREIGN KEY (designation_id) REFERENCES designations(id);
```
