# Database (DB):
- Any collection of related information.

## Database Management Systems (DBMS)
- A special software program that helps users create and maintain a database
  - Makes it easy to manage large amounts of information
  - Handles Security & Backups
  - Importing/exporting data
  - Concurrency
  - Interacts with software applications
    - Programming Languages
  
### Relational Databases (SQL)
- Organize data into one or more tables
  - Each table has columns and rows
  - A unique key identifies each row
    - Row contains the information about a single object
    - Column conatins inforamtion about a single attribute
  
#### Database Queries
- Queries are requests made to the database management system for specific information

### Types of Keys:
#### Super Key:
- A super key is a group of single or multiple keys which identifies rows in a table.
#### Primary Key:
- A primary key, also called a primary keyword, is a column in a relational database table that's distinctive for each record.
#### Candidate Key:
- It is a set of attributes that uniquely identify tuples in a table. Candidate Key is a super key with no repeated attributes.
#### Alternate Key:
- It is a column or group of columns in a table that uniquely identify every row in that table.
#### Foreign Key:
- It is a column that creates a relationship between two tables. The purpose of Foreign keys is to maintain data integrity and allow navigation between two different instances of an entity.
#### Compound Key: 
- It has two or more attributes that allow you to uniquely recognize a specific record. It is possible that each column may not be unique by itself within the database.
#### Composite Key: 
- It is a combination of two or more columns that uniquely identify rows in a table. The combination of columns guarantees uniqueness, though individual uniqueness is not guaranteed.
#### Surrogate Key:
- An artificial key which aims to uniquely identify each record is called a surrogate key. These kind of key are unique because they are created when you don't have any natural primary key.

### Structured Query Language [(SQL)](https://www.w3schools.com/sql/default.asp):
- SQL is actually a hybrid language, it's basically 4 types of languages in one
  -  **Data Query Language (DQL)**
    -  Used to query the database for information.
    -  Get information that is already stored there
  - **Data Definition Language (DDL)**
    - Used for defining database schemas.
  - **Data Control Language (DCL)**
    - Used for controlling access to the data in the database.
    - User & permissions management
  - **Data Manipulation Language (DML)**
    - Used for inserting, updating and deleting data from the data
   
## Tables:
### SQL CREATE TABLE Statement:
- The `CREATE TABLE` statement is used to create a new table in a database.
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```
- Creating a Table using another table.
```sql
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....;
```
### SQL DROP TABLE Statement:
- The `DROP TABLE` statement is used to drop an existing table in a database.
```sql
DROP TABLE table_name;
```
- To delete Data inside table:
  - The `TRUNCATE TABLE` statement is used to delete the data inside a table, but not the table itself.
```sql
TRUNCATE TABLE table_name;
```

### ALTER TABLE Statement
- The `ALTER TABLE` statement is used to add, delete, or modify columns in an existing table. It can also be used to add and drop various constraints on an existing table.
```sql
-- Add Column
ALTER TABLE table_name
ADD column_name datatype;

-- Drop Column
ALTER TABLE table_name
DROP COLUMN column_name;

-- Rename Column
ALTER TABLE table_name
RENAME COLUMN old_name to new_name;

-- Modify Datatype
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

### INSERT INTO Statement:
- The `INSERT INTO` statement is used to insert new records in a table. Two ways to insert the data into the table:
  - By specifying the column name and values to be inserted
```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```
  - If adding values to all columns dont need to specify column names, but oder the data according to the order of the columns present in the table.
```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```
### Constraints:
- Constraints can be specified when the table is created with the `CREATE TABLE` statement, or after the table is created with the `ALTER TABLE` statement.
```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    column3 datatype constraint,
    ....
);
```
#### NOT NULL Constraint:
- The `NOT NULL` constraint enforces a column to NOT accept NULL values.
#### UNIQUE Constraint:
- The `UNIQUE` constraint ensures that all values in a column are different. Both the `UNIQUE` and `PRIMARY KEY` constraints provide a guarantee for uniqueness for a column or set of columns.
- A `PRIMARY KEY` constraint automatically has a `UNIQUE` constraint. However, you can have many `UNIQUE` constraints per table, but only one `PRIMARY KEY` constraint per table.
#### DEFAULT Constraint:
- The `DEFAULT` constraint is used to set a default value for a column and will be passed as a value if no input is provided.

#### AUTO INCREMENT Field:
- Auto-increment allows a unique number to be generated automatically when a new record is inserted into a table. Not exactly a constraint but is passed into the table and this is normally used for a primary key.

### UPDATE Statement:
- The `UPDATE` statement is used to modify the existing records in a table.
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

-- If we omit WHERE -> all the values are updated.
```
### DELETE Statement:
- The `DELETE` statement is used to delete existing records in a table.
```sql
DELETE FROM table_name WHERE condition;
-- If we Omit WHERE -> all values are deleted
```

## SQL SELECT Statement:
- The `SELECT` statement is used to select data from a database. The data returned is stored in a result table, called the result-set.
```sql
-- Select certain columns from the table
SELECT column1, column2, ...
FROM table_name;

-- Select the whole table
SELECT * FROM table_name;
```

### ORDER BY Keyword:
- The `ORDER BY` keyword is used to sort the result-set in ascending or descending order.
- If we don't specify the order it needs to be returned in, it defualts to acending order.
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;

-- Also we could be selective in ordering the table:
-- In this, we first order according to columnx, if there is a clash then we order those objects according to columny
SELECT *
FROM table_name
ORDER BY columnx, columny;
```

### LIMIT Keyword:
- The `LIMIT` Keyword is used to show only a specified number of table entries
```sql
-- This only shows n nummber of Objects in the Table.
SELECT *
FROM table_name
LIMIT n;
```

### WHERE Clause:
- The `WHERE` clause is used to filter records. It is used to extract only those records that fulfil a specified condition.
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;

-- Operators which can be used in the WHERE Statements
=            Equal
>            Greater than
<            Less than
>=           Greater than or equal
<=           Less than or equal
<>           Not equal

BETWEEN      Between a certain range
  WHERE column_name BETWEEN value1 AND value2;
LIKE         Search for a pattern
  WHERE column_name LIKE pattern;
IN           To specify multiple possible values for a column
  WHERE column_name IN (value1, value2, ...);
```

### AS clause:
- The `AS` command is used to rename a column or table with an alias.
```sql
SELECT CustomerID AS ID, CustomerName AS Customer
FROM Customers;
```

### SELECT DISTINCT Statement:
- The `SELECT DISTINCT` statement is used to return only distinct (different) values.
```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

### GROUP BY Statement:
- The `GROUP BY` statement groups rows that have the same values into summary rows, like "find the number of customers in each country".
- The `GROUP BY` statement is often used with aggregate functions (`COUNT()`, `MAX()`, `MIN()`, `SUM()`, `AVG()`) to group the result-set by one or more columns.
```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);
```

## [MySQL Functions](https://www.w3schools.com/sql/sql_ref_mysql.asp):
- MySQL has many built-in functions which can be used to find the various values we need like SUM, AVG, etc.

## Wildcards:

### LIKE Operator:
The `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column.
There are two wildcards often used in conjunction with the `LIKE` operator:
- The percent sign (%) represents zero, one, or multiple characters
- The underscore sign (_) represents one, single character

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column LIKE pattern;

-- Using %
-- In this example, we use this wildcard to specify that there can be nay number of characters before LLC but if this kind of pattern is present in the table client and in the column client_name then we will return it.
SELECT *
FROM client
WHERE client_name LIKE '%LLC';

-- Using _
-- In this example, we use _ to specify one character space. In this example, the person with thier birthday in october is shown as a result
SELECT *
FROM employee
WHERE birth_date LIKE '____-10%';
```

## UNION Operator:
The `UNION` operator is used to combine the result-set of two or more `SELECT` statements.
- Every `SELECT` statement within `UNION` must have the same number of columns
- The columns must also have similar data types
- The columns in every `SELECT` statement must also be in the same order
```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

## JOIN Clause:
- A `JOIN` clause is used to combine rows from two or more tables, based on a related column between them.
- table1 -> Left and table2 -> Right
- Here are the different types of the JOINs in SQL:

<img width="864" alt="Joins" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/ecb41b2b-1dd4-4826-b1bc-ac4b40294954">

  - `(INNER) JOIN`: Returns records that have matching values in both tables
```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```
  - `LEFT (OUTER) JOIN`: Returns all records from the left table, and the matched records from the right table
```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```
  - `RIGHT (OUTER) JOIN`: Returns all records from the right table, and the matched records from the left table
```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```
  - `FULL (OUTER) JOIN`: Returns all records when there is a match in either left or right table
```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name
WHERE condition;
```

## Nested Queries:
- Nested queries are a way to perform more complex queries by embedding one query within another.
- First the innermost statement is executed then the next one [IN -> OUT].
### SQL IN Operator:
- The `IN` operator allows you to specify multiple values in a WHERE clause. It is a shorthand for multiple `OR` conditions.
```sql
-- For executing multiple OR statements
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);

-- For executing nested Queries
SELECT column_name(s)
FROM table_name
WHERE column_name IN (SELECT STATEMENT);
```
## ON DELETE STATEMENT:
- We use DELETE to remove a certain object or column in the table. But ON DELETE is a special attribute which tells the table what values need to be present if the key is deleted.

1) `ON DELETE CASCADE` constraint is used in MySQL to delete the rows from the child table automatically when the rows from the parent table are deleted.
2) `ON DELETE SET NULL` constraint deletes or updates the row from the parent table and set the foreign key column or columns in the child table to NULL.

> Always use CASCADE if the primary key of a table is being affected as the key can't be null. 
```sql
-- If we remove a manager then the values corresponding to the manages will get set to null in SET NULL and DELETED if CASCADED 
-- SET NULL
CREATE TABLE branch (
  branch_id INT PRIMARY KEY,
  branch_name VARCHAR(40),
  mgr_id INT,
  mgr_start_date DATE,
  FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL
);

--  CASCADE
CREATE TABLE branch_supplier (
  branch_id INT,
  supplier_name VARCHAR(40),
  supply_type VARCHAR(40),
  PRIMARY KEY(branch_id, supplier_name),
  FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE
);
```

## Trigger:
- Triggers will be helpful when we need to execute some events automatically on certain desirable scenarios.
```sql
-- Create Trigger
CREATE TRIGGER schema.trigger_name  
ON table_name  
AFTER  {INSERT, UPDATE, DELETE}  
[NOT FOR REPLICATION]  
AS  
{SQL_Statements}

-- Drop Trigger
DROP TRIGGER [IF EXISTS] schema_name.trigger_name;  
```

## Common Table Expression:
- CTEs act as virtual tables (with records and columns) that are created during query execution, used by the query, and deleted after the query executes.
```sql
-- Syntax:
[WITH  [, …]]  
::=
cte_name [(column_name [, …])]
AS (cte_query) 

-- Example
-- We need to execute these queries together, or else the select won't work on its own
WITH CTE Employee as
(SELECT FirstName, LastName, Gender, Salary , COUNT (gender) OVER (PARTITION by Gender) as TotalGender , AVG (Salary) OVER (PARTITION BY Gender) as AvgSalary
FROM SQLTutorial..EmployeeDemographics emp
JOIN SQLTutorial..EmployeeSalary sal
ON emp.EmployeeID = sal. EmployeeID
WHERE Salary > '45000'
)
SELECT * FROM CTE_EMPLOYEE;

```
