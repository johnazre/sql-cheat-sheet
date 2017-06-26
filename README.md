# sql-cheat-sheet

## Index
* [How do I start `psql`](#how-to-start-psql)
* [How do I create a database in `psql`](#how-to-create-db)
* [How do I connect to a database in `psql`](#connect-to-db)
* [How do I create a table in `psql`](#create-a-table)
* [How do I data into a table in `psql`](#insert-data-into-table)
* [How do I update data a table in `psql`](#update-data-inside-table)
* [How do I delete data from a table in `psql`](#delete-data-from-table)
* [How do I query data from a table in `psql`](#query-data-from-table)
* [How do I get a list of tables in `psql`](#get-list-of-tables)
* [How do I get a list of table columns in `psql`](#get-columns-of-tables)
* [How do I add a columnt in `psql`](#add-a-new-column)
* [How do I get the total number of entries in a table in `psql`](#total-number-of-entries)
* [How do I get the sum of values of a column in `psql`](#sum-of-values)
* [How do I get the average of values of a column in `psql`](#get-average-of-values)


### How to start PSQL?<a id="how-to-start-psql"></a>
* Open terminal window
* Type `psql postgres` OR `psql name-of-db`

### How to create a database?<a id="how-to-create-db"></a>
* From inside of `psql`, run `CREATE DATABASE testdb`
* Alternate option would be to run `createdb testdb` from the terminal.

### How to connect to a database?<a id="connect-to-db"></a>
* From inside of `psql`, run `\c testdb`

### How to create a table?<a id="create-a-table"></a>
* From inside of `psql`, run `CREATE TABLE people(id SERIAL, name VARCHAR(255), age INT);`

### How to insert data into table?<a id="insert-data-into-table"></a>
* From inside of `psql`, run `INSERT INTO people VALUES(DEFAULT, 'james', 44);`
* From inside of `psql`, run `INSERT INTO people(name, age) VALUES('james', 44);`

### How to update data inside table?<a id="update-data-inside-table"></a>
* From inside of `psql`, run `UPDATE people SET age = 33 WHERE name = 'james';`

### How to delete data from table?<a id="delete-data-from-table"></a>
* From inside of `psql`, run `DELETE FROM people WHERE name = 'james';`

### How to query data from table?<a id="query-data-from-table"></a>
* From inside of `psql`, run `SELECT * FROM people;`
* From inside of `psql`, run `SELECT name FROM people;`
* From inside of `psql`, run `SELECT * FROM people WHERE age > 30;`

### How to get a list of tables?<a id="get-list-of-tables"></a>
* From inside of `psql`, run `\d`

### How to get a columns from a table?<a id="get-columns-of-tables"></a>
* From inside of `psql`, run `\d people`

### How to get add column to an existing table?<a id="add-a-new-column"></a>
* From inside of `psql`, run `ALTER TABLE people ADD COLUMN hair VARCHAR(50);`

### How to get a total number of entries in a table?<a id="total-number-of-entries"></a>
* From inside of `psql`, run `SELECT COUNT(*) FROM people;`
* From inside of `psql`, run `SELECT COUNT(*) FROM people WHERE age < 40;`

### How to sum the values in a single column?<a id="sum-of-values"></a>
* From inside of `psql`, run `SELECT SUM(age) FROM people;`

### How to average the values in a single column?<a id="get-average-of-values"></a>
* From inside of `psql`, run `SELECT AVG(age) FROM people;`