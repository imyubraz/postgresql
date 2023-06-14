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

```
INSERT INTO test.students(first_name, last_name, house_number, phone, email, grad_year)
VALUES('Yubraj', 'Poudel', 22, 987654321, 'imyubraz@gmail.com', 2023)
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

