# SQL Commands and Concepts

A quick-reference guide to essential SQL commands, organized by category.

---

## Table of Contents

**Database Operations**
1. [Create Database](#1-create-database)
2. [Show Databases](#2-show-databases)
3. [Show Schemas](#3-show-schemas)
4. [Drop Database](#4-drop-database)
5. [Use Database](#5-use-database)

**Writing SQL**

6. [Single-line Comments](#6-single-line-comments)
7. [Multi-line Comments](#7-multi-line-comments)

**Data Types & Table Structure**

8. [Data Types in SQL](#8-data-types-in-sql)
9. [Primary Key Concept](#9-primary-key-concept)
10. [Create Table](#10-create-table)
11. [Show Tables](#11-show-tables)
12. [Show Columns From](#12-show-columns-from)
13. [Add New Column in the Table](#13-add-new-column-in-the-table)
14. [Modify Column in the Table](#14-modify-column-in-the-table)
15. [Delete Column in the Table](#15-delete-column-in-the-table)
16. [Rename Table](#16-rename-table)
17. [Drop Table](#17-drop-table)

**Querying & Modifying Data**

18. [Select](#18-select)
19. [Insert Into Table](#19-insert-into-table)
20. [Insert Into Multiple Rows](#20-insert-into-multiple-rows)
21. [Using WHERE with SELECT](#21-using-where-with-select)
22. [Update](#22-update)
23. [Order By](#23-order-by)
24. [Delete](#24-delete)
25. [Group By](#25-group-by)

---

## Database Operations

### 1. Create Database
Creates a new database in SQL.
```sql
CREATE DATABASE database_name;
```

### 2. Show Databases
Lists all databases available in the SQL server.
```sql
SHOW DATABASES;
```

### 3. Show Schemas
Displays the schemas (or databases) in the current database.
```sql
SHOW SCHEMAS;
```

### 4. Drop Database
Deletes an existing database.

> ⚠️ **Use caution** — this removes all data within the database, and it cannot be undone.

```sql
DROP DATABASE database_name;
```

### 5. Use Database
Switches the current database to the specified one.
```sql
USE database_name;
```

---

## Writing SQL

### 6. Single-line Comments
SQL comments are useful for leaving notes in your code. A single-line comment begins with `--`.
```sql
-- This is a single-line comment
```

### 7. Multi-line Comments
Multi-line comments begin with `/*` and end with `*/`.
```sql
/* 
This is a 
multi-line comment 
*/
```

---

## Data Types & Table Structure

### 8. Data Types in SQL
Data types define the kind of data a column can hold in a table.

| Type | Description |
|---|---|
| `INT` | Integer (whole number) |
| `VARCHAR(n)` | String with a maximum length of `n` |
| `DATE` | Date in `YYYY-MM-DD` format |
| `DECIMAL(m,n)` | Decimal number with `m` total digits, `n` after the decimal point |
| `BOOLEAN` | Stores `TRUE` or `FALSE` |

### 9. Primary Key Concept
A primary key uniquely identifies each record in a table. It must be unique and cannot contain `NULL` values.
```sql
CREATE TABLE table_name (
    column_name INT PRIMARY KEY
);
```

### 10. Create Table
Creates a new table with defined columns and their data types.
```sql
CREATE TABLE table_name (
    column1_name column1_data_type,
    column2_name column2_data_type,
    ...
);
```

### 11. Show Tables
Lists all tables in the currently selected database.
```sql
SHOW TABLES;
```

### 12. Show Columns From
Displays the column structure of a specific table.
```sql
SHOW COLUMNS FROM table_name;
```

### 13. Add New Column in the Table
Adds a new column to an existing table.
```sql
ALTER TABLE table_name
ADD column_name data_type;
```

### 14. Modify Column in the Table
Changes the data type of an existing column.
```sql
ALTER TABLE table_name
MODIFY column_name new_data_type;
```

### 15. Delete Column in the Table
Removes a column from an existing table.
```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

### 16. Rename Table
Renames an existing table in the database.
```sql
ALTER TABLE old_table_name RENAME TO new_table_name;
```

### 17. Drop Table
Deletes an existing table in the database.
```sql
DROP TABLE table_name;
```

---

## Querying & Modifying Data

### 18. Select
Retrieves data from one or more tables.
```sql
SELECT column_name(s) FROM table_name;
```

**Select all columns:**
```sql
SELECT * FROM table_name;
```

### 19. Insert Into Table
Inserts one or more rows into a table in the database.
```sql
INSERT INTO table_name (column1, column2, ...) 
VALUES (value1, value2, ...);
```

### 20. Insert Into Multiple Rows
Inserts multiple rows into a table in the database.
```sql
INSERT INTO table_name (column1, column2, ...) 
VALUES (value1, value2, ...),
       (value3, value4, ...),
       (value5, value6, ...);
```

### 21. Using WHERE with SELECT
Filters the results of a SELECT statement based on conditions specified in the WHERE clause.
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Example:** Suppose we have a table called `employees` with columns `id`, `name`, `department`, and `salary`. We want to retrieve the name and salary of all employees in the Sales department who earn more than $50,000.
```sql
SELECT name, salary
FROM employees
WHERE department='Sales' AND salary > 50000;
```

### 22. Update
Updates existing records in a table based on a condition.
```sql
UPDATE table_name
SET column_name = new_value
WHERE condition;
```

**Example:**
```sql
UPDATE Student
SET FIRST_NAME = 'John'
WHERE Student_ID = 1;
```

### 23. Order By
Sorts the result set in ascending or descending order based on one or more columns.
```sql
SELECT column_name(s)
FROM table_name
ORDER BY column_name [ASC|DESC];
```

**Example:**
```sql
SELECT * 
FROM Student
ORDER BY FIRST_NAME ASC;
```

### 24. Delete
Deletes records from a table based on a condition.
```sql
DELETE FROM table_name
WHERE condition;
```

**Example:**
```sql
DELETE FROM Student
WHERE Student_ID = 1;
```

### 25. Group By
Groups rows that have the same values into summary rows, often used with aggregate functions like `COUNT`, `SUM`, `AVG`, etc.
```sql
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name;
```

**Example:**
```sql
SELECT FIRST_NAME, COUNT(*)
FROM Student
GROUP BY FIRST_NAME;
```
