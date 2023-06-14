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

