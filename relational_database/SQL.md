# SQL Reference Guide

## Basic Commands

### Show Databases
~~~
SHOW DATABASES;
~~~
- Lists all available databases.

### Select a Database
~~~
USE <database_name>;
~~~
- Switches to a specific database.

### Show Tables
~~~
SHOW TABLES;
~~~
- Lists all tables in the selected database.

### Describe a Table
~~~
DESC <table_name>;
~~~
- Displays the structure and description of a table.

## Create Commands

### Create a Database
~~~
CREATE DATABASE <database_name>;
~~~
- It will create new database.

### Create a Table
~~~
CREATE TABLE <table_name> ( <column_name_1> [datatype] <constraint>, <column_name_2> [datatype], ... );
~~~


## Insert and Select Data

###  Insert Data
~~~
INSERT INTO <table_name> (col1, col2, ...) VALUES (value1, value2, ...);
~~~
### Select Data
~~~
SELECT <column_name> FROM <table_name>;
~~~
- Use `*` to select all columns.

### Example: Insert Multiple Rows
~~~
INSERT INTO table_name (Name, DoB, Gender) VALUES
("Tanzimul", "2022-01-02", "Male"),
("Neha", "2019-03-04", "Female"),
("King", "1999-01-04", "Other");
~~~
### Filtering Data with Conditions
~~~
SELECT * FROM <table_name> WHERE <conditions>;
~~~

### Examples:
~~~
SELECT * FROM second WHERE DoB > '2000-01-01' AND Gender = 'Female';

SELECT * FROM second WHERE Name LIKE "_a%"; (Names starting with 'a');

SELECT * FROM second WHERE Gender = 'Female' ORDER BY DoB DESC LIMIT 2;
~~~


## Update and Delete Data

### Update Data
~~~
UPDATE <table_name> SET <column_name> = <value> WHERE <conditions>;
~~~

### Example:
~~~
UPDATE Actors SET FirstName = "RJ", NetWorthInMillions = 1000 WHERE Id = 6;
~~~

### Delete Data
~~~
DELETE FROM <table_name> WHERE <conditions>;
~~~
### Example:

~~~
DELETE FROM Names WHERE name LIKE "%e%" ORDER BY name LIMIT 1;

Use DELETE FROM <table_name>;
~~~

- to delete all rows.



## Alter Table

### Change Column
~~~
ALTER TABLE <table_name> CHANGE <old_column_name> <new_column_name> [datatype/constraint];
~~~
#### Example:
~~~
ALTER TABLE Actors CHANGE NetWorthInMillions NetWorth DECIMAL(10,2);
~~~
### Add a Column
~~~
ALTER TABLE <table_name> ADD <column_name> [datatype/constraint];
~~~
#### Example:
~~~
ALTER TABLE Actors ADD MiddleName VARCHAR(10) AFTER FirstName;
~~~
### Drop a Column
~~~
ALTER TABLE <table_name> DROP <column_name>;
~~~



## Aggregation Functions

### Examples:
~~~
SELECT SUM(NetWorth) FROM Actors;
SELECT AVG(Score) FROM Students2 WHERE Marital_Status = 'Married';
SELECT COUNT(*) AS "No. of Single People" FROM Students2 WHERE Marital_Status = 'Single';
SELECT DISTINCT Score FROM Students2;
~~~
### Group By and Having
~~~
SELECT Marital_Status, COUNT(*) FROM Students2 GROUP BY Marital_Status;
SELECT DoB, COUNT(*) FROM Students2 GROUP BY DoB HAVING DoB > '1998-04-26';
~~~
## Joins

### Inner Join
~~~
SELECT * FROM <table1> INNER JOIN <table2> ON <join_condition>;
~~~
### Left Join
~~~
SELECT * FROM <table1> LEFT JOIN <table2> ON <join_condition>;
~~~

### Right Join
~~~
SELECT * FROM <table1> RIGHT JOIN <table2> ON <join_condition>;
~~~
### Using Clause
~~~
SELECT FirstName, DoB, URL FROM Actors LEFT JOIN DigitalAssets USING(Id);
~~~
- Use `USING(column_name)` only if both tables have the same column name.

### Cartesian Product
~~~
SELECT FirstName, DoB, URL FROM Actors, DigitalAssets WHERE Actors.Id = DigitalAssets.Id;
~~~
- Matches every row from Table A with every row from Table B.

### Self Join
~~~
SELECT e1.employee_name, e2.employee_name AS Manager
FROM Employees e1
INNER JOIN Employees e2
ON e1.manager_id = e2.id;
~~~

## Union Queries
~~~
(SELECT * FROM Students2) UNION (SELECT * FROM TempActors);
~~~

- Combines the results of two queries. Column counts must match.

## Ordering and Limit
~~~
SELECT * FROM <table_name> ORDER BY <column_name> ASC|DESC LIMIT <number>;
~~~

- Example: `SELECT * FROM Students2 ORDER BY DoB DESC LIMIT 5;`

## Aliases and Concatenation

### Alias
~~~
SELECT DoB AS "Date of Birth" FROM Actors;
~~~
### Concatenate Columns

~~~
SELECT CONCAT(FirstName, ' ', SecondName) AS FullName FROM Actors;
~~~





