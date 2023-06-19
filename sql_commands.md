# SQL Commands (PostgreSQL)

## Create database

```
CREATE database <db_name>
```

```
CREATE database test
```

## Drop database

```
DROP database <db_name>
```

```
DROP database test
```

> Make sure to disconnect db first before dropping it

## Create Schema

```
CREATE SCHEMA test
```

> make sure to connect to db first (using pgadmin ui) if it got disconnected for any reason

## Create Table

```
CREATE table <schema_name>.<table_name>();
```

```
CREATE table test.employee(
	id int primary key,
	emp_name varchar(50)
);
```
```
CREATE TABLE test.students (
	student_id SERIAL PRIMARY KEY,
	first_name VARCHAR(30) NOT NULL,
	last_name VARCHAR(30) NOT NULL,
	house_number INTEGER,
    phone VARCHAR(20) NOT NULL UNIQUE,
	email VARCHAR(255) UNIQUE,
	grad_year INTEGER
);
```

## Insert data into table

```
INSERT INTO <schema_name>.<table_name>(<columns>) values(<corresponding_values>);
```

```
INSERT INTO test.employee(id, emp_name) values(1, 'Yubraj');
```

## View data

```
SELECT * from <schema_name>.<table_name>;
```

```
SELECT * from test.employee;
```

## Truncate Table

- Truncate clear out all data/rows maintaining structure of table.
- We cannot ROLLBACK if we truncate table.

```
TRUNCATE <schema_name>.<table_name>
```

```
TRUNCATE test.employee;
```

## Altering Column

```
ALTER table <schema_name>.<table_name>
```

```
ALTER table test.employee
ALTER column emp_name type varchar(100)
```

## Renaming Table Name

```
ALTER table <schema_name>.<table_name>
```

```
ALTER table test.employee
RENAME to emp
```

> Table's name "employee" will changed to "emp"


## Datatypes in PostgreSQL

- Ref : https://www.postgresql.org/docs/current/datatype.html

- 

```
CREATE TABLE test.students (
	student_id SERIAL PRIMARY KEY,
	first_name VARCHAR(30) NOT NULL,
	last_name VARCHAR(30) NOT NULL,
	house_number INTEGER,
    phone VARCHAR(20) NOT NULL UNIQUE,
	email VARCHAR(255) UNIQUE,
	grad_year INTEGER
);
```

In this query, the columns are defined as follows:

	- student_id is the primary key column, and its value will be automatically generated using the SERIAL data type.
	- first_name and last_name are both VARCHAR(30) columns and are set as NOT NULL, indicating that they must have a value.
	- house_number is an optional column of type INTEGER, allowing for storing numeric house numbers.
	- phone is a VARCHAR(20) column that must have a value (NOT NULL) and must be unique (UNIQUE constraint).
	- email is a VARCHAR(255) column that allows for storing email addresses. It must be unique (UNIQUE constraint).
	- grad_year is an optional column of type INTEGER, allowing for storing graduation years.

- Comparisions
	- In SQL AUTO INCREMENT , in PostgreSQL SERIAL
	- In SQL NUMBER(10) , in PostgreSQL NUMERIC(10)


## PostgreSQL DML (Data Manipulation Language)

- DML includes insert, update & delete.

### INSERT

```
INSERT INTO <schema_name>.<table_name> (column1, column2, column3) VALUES (value1, value2, value3)
```

- One data Insertion

```
INSERT INTO test.students(first_name, last_name, house_number, phone, email, grad_year)
VALUES('Yubraj', 'Poudel', 22, 987654321, 'imyubraz@gmail.com', 2023)
```

- Multiple data Insertion

```
INSERT INTO test.students(first_name, last_name, house_number, phone, email, grad_year)
VALUES ('Yubraj', 'Poudel', 22, 987654321, 'imyubraz@gmail.com', 2023),
('Roshan', 'Neupane', 22, 987654321, 'imyubraz@gmail.com', 2023)
```

### UPDATE

```
UPDATE <schema_name>.<table_name> SET column1 = value1,
column2 = value2,
column3 = value3
WHERE condition...;
```

```
UPDATE test.students SET student_id=2, 
email= 'roshanneupane600@gmail.com' 
WHERE student_id=3
```

### DELETE

```
DELETE FROM <schema_name>.<table_name>
WHERE condition...;
```

```
DELETE FROM test.students where student_id=2;
```

> If condition is not mentioned at the end, all data will be deleted.

> We can ROLLBACK if we've used DELETE command but not in case of TRUNCATE command.

## PostgreSQL DQL (Data Query Language)

### SELECT 

- First Inserting in students table (in test schema)

```
INSERT INTO test.students(first_name, last_name, house_number, phone, email, grad_year)
VALUES ('Yubraj', 'Poudel', 22, 988654321, 'iamyubraz@gmail.com', 2023),
('Roshan', 'Neupane', 22, 98345698765, 'roshanneupane600@gmail.com', 2023),
('Brajesh', 'Mandal', 23, 9812345671, 'brajesh@gmail.com', 2023),
('Roshan', 'Neupane', 22, 9812874561, 'roshan@gmail.com', 2023),
('Kisna', 'Basnet', 23, 9812345679, 'kisna@gmail.com', 2023)
```

- Fetch all columns using SELECT

```
SELECT * FROM test.students
```

- Fetch selective columns using SELECT

```
SELECT column_name_1, column_name_2 FROM test.students
```
```
SELECT first_name last_name FROM test.students
```

- Fetch Distinct rows in column(s)

```
SELECT DISTINCT first_name, last_name FROM test.students
```
> It will show first_name & last_name once, if duplicate data exists

```
SELECT DISTINCT * FROM test.students
```
> It will show distint rows. May be some columns have duplicate data but it will be distinct as a entire row.

- Conditional Fetching using WHERE clause

	- Get all columns of row(s) as per condition mentioned in WHERE clause:

	```
	SELECT * FROM test.students WHERE student_id=10
	```

	```
	SELECT * FROM test.students WHERE student_id IN (10,11,12)
	```

	- Get selective columns of row(s) as per condition mentioned in WHERE clause:

	```
	SELECT first_name, last_name FROM test.students WHERE student_id=10
	```

	```
	SELECT first_name, last_name FROM test.students WHERE student_id IN (10,11,12)
	```

- Sorting while fetching using ORDER BY clause:

> By default fetched rows/recordes are ordered in ascending manner by primary key.

```
SELECT * FROM test.students ORDER BY student_id DESC
```
> It will show all columns data sorted descending according student_id

```
SELECT * FROM test.students ORDER BY student_id ASC
```
> It will show all columns data sorted accending according student_id

```
SELECT first_name, last_name FROM test.students ORDER BY first_name ASC
```
> It will first_name & last_name columns data sorted descending according student_id

- Limit no. of rows in output using LIMIT keyword

```
SELECT * FROM test.students LIMIT 3
```
> It will give 3 rows, all columns in output

```
SELECT first_name, phone FROM test.students LIMIT 5
```
> It will give 5 rows, first_name & phone columns in output

```
SELECT first_name, phone FROM test.students ORDER BY first_name desc LIMIT 3
```
> It will give top 3 rows (with first_name & phone columns) when ordered in descending manner, or bottom 3 rows when ordered in ascending manner
> Note: LIMIT keyword should used after ORDER BY clause when used together

- Limiting no. of rows in output using FETCH

```
SELECT * FROM test.students
FETCH FIRST 4 row only
```
> Give first 4 records

```
SELECT * FROM test.students
ORDER BY first_name DESC
FETCH FIRST 4 row only
```
> Give last 4 records (since ordered in descending manner)


- Excluding first fetched row(s) using OFFSET keyword

```
SELECT * FROM test.students OFFSET 2
```
> Exclude first 2 rows (or start fetching from 3rd record) while fetching

```
SELECT first_name, phone FROM test.students ORDER BY first_name desc LIMIT 3 OFFSET 1
```
> Exclude first record (or start fetching from 2nd record) while fetching
> Note: OFFSET keword should used after LIMIT keyword when used together

- GROUP BY clause

> primary_key must appear in the GROUP BY clause or GROUP BY clause must be used in an aggregate function

```
SELECT COUNT(*) FROM test.students
GROUP BY grad_year
```

```
SELECT COUNT(*), grad_year FROM test.students
GROUP BY grad_year
```
> Its good to select column which is used to group by while fetching to ease understanding output. (eg: grad_year column here)

```
SELECT COUNT(*), grad_year FROM test.students
GROUP BY grad_year
ORDER BY grad_year ASC
```
> Using ORDER BY clause along GROUP BY

- HAVING clause

> HAVING clause is always used along with GROUP BY to give condition.

```
SELECT COUNT(*), grad_year FROM test.students
GROUP BY grad_year
HAVING grad_year > 2020
```

```
SELECT COUNT(*), grad_year FROM test.students
GROUP BY grad_year
HAVING grad_year = 2024
```

### SQL JOINS

- We use SQL joins to connect two or more tables in Relational Databases. 

- Types of SQL joins : INNER JOIN, RIGHT OUTER JOIN, LEFT OUTER JOIN, FULL OUTER JOIN, CROSS JOIN, LEFT JOIN, RIGHT JOIN, Self join, FULL JOIN, FULL OUTER joins, RIGHT OUTER joins

- First adding two new tables Students_A (students of class A) & Students_B (students of class B)

	- create Students_A table

	```
	CREATE TABLE test.Students_A (
		student_id SERIAL PRIMARY KEY,
		first_name VARCHAR(30) NOT NULL,
		last_name VARCHAR(30) NOT NULL,
		age INTEGER,
		phone VARCHAR(20) NOT NULL UNIQUE,
		email VARCHAR(255) UNIQUE,
		grad_year INTEGER
	);
	```

	- Insert records in student_a/Student_A table
	```
	INSERT INTO test.students_a(first_name, last_name, age, phone, email, grad_year)
	VALUES ('Yubraj', 'Poudel', 23, 9817132325, 'imyubraz@gmail.com', 2023),
	('Roshan', 'Neupane', 22, 987654321, 'roshanneupane600@gmail.com', 2025)
	```

	- View all records in student_a/Student_A table
	```
	SELECT * FROM test.students_a
	```

	- create Students_B/students_b table (with same structure and data ad student_a table, basically copying entire table, can be used for backup purpose)

	```
	CREATE TABLE test.students_b
	as
	SELECT * FROM test.students_a
	```
	>  Note: column constraints will not be valid anymore


	- or we can create Students_B/students_b table by following students_a table's structure only not copy entire data

	```
	CREATE TABLE test.students_b
	as
	SELECT * FROM test.students_a WHERE 1=2
	```
	> We can give any condition (falsy condition) in where clause which should result 0 no. of rows
	>  Note: column constraints will not be valid anymore

	- or Create table manually (recommended)
	```
	CREATE TABLE test.Students_B (
		student_id SERIAL PRIMARY KEY,
		first_name VARCHAR(30) NOT NULL,
		last_name VARCHAR(30) NOT NULL,
		age INTEGER,
		phone VARCHAR(20) NOT NULL UNIQUE,
		email VARCHAR(255) UNIQUE,
		grad_year INTEGER
	);
	```

	- Now Insert records in student_b/Student_B table as well

	```
	INSERT INTO test.students_b(first_name, last_name, age, phone, email, grad_year)
	VALUES ('Sujan', 'Poudel', 23, 985612346, 'poudelsujan@gmail.com', 2024),
	('Kisna', 'Basnet', 24, 987654321, 'kisnabasnet@gmail.com', 2024),
	('Gobind', 'Joshi', 22, 980654321, 'gobindjoshi@gmail.com', 2024)
	```

	- Now Insert records in student_b/Student_B table as well

	```
	INSERT INTO test.students_b(first_name, last_name, age, phone, email, grad_year)
	VALUES ('Sujan', 'Poudel', 23, 985612346, 'poudelsujan@gmail.com', 2024),
	('Kisna', 'Basnet', 24, 987654321, 'kisnabasnet@gmail.com', 2024),
	('Gobind', 'Joshi', 22, 980654321, 'gobindjoshi@gmail.com', 2024)
	```

	- Create registration table which holds student's registration data

	```
	CREATE TABLE IF NOT EXISTS test.registration (
		student_id INTEGER NOT NULL,
		first_name VARCHAR(30) NOT NULL,
		last_name VARCHAR(30) NOT NULL,
		age INTEGER,
		status VARCHAR(20) NOT NULL,
		start_date DATE
	);
	```



- Joins in created tables
	- Inner Join : id/data common in both Students_A & Students_B. (matching records only)
	- Left Join : All left table records + matching records
	- Right Join : All right table records + matching records
	- Full join : All left table records + matching records + All right table records
	- Cross Join : Cartesian product of records (left X right)
	- Self Join


	













