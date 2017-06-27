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
* [How do I get part of a date field in `psql`](#get-part-of-date-field)

<h3 id="how-to-start-psql">How to start PSQL?</h3>
* Open terminal window
* Type `psql (name of the database)`

<h3 id="how-to-create-db">How to create a database?</h3>
* From inside of `psql`, run `CREATE DATABASE db-name`
* Alternate option would be to run `createdb db-name` from the terminal.

<h3 id="connect-to-db">How to connect to a database?</h3>
* From inside of `psql`, run `\c db-name`

<h3 id="create-a-table">How to create a table?</h3>
* From inside of `psql`, run `CREATE TABLE db-name(id SERIAL, whateverElseWithType);`

<h3 id="insert-data-into-table">How to insert data into table?</h3>
* From inside of `psql`, run `INSERT INTO table-name VALUES(DEFAULT, theRest);`
* From inside of `psql`, run `INSERT INTO people(name, age) VALUES('james', 44);`

<h3 id="update-data-inside-table">How to update data inside table?</h3>
* From inside of `psql`, run `UPDATE people SET age = 33 WHERE name = 'james';`

<h3 id="delete-data-from-table">How to delete data from table?</h3>
* From inside of `psql`, run `DELETE FROM people WHERE name = 'james';`

<h3 id="query-data-from-table">How to query data from table?</h3>
* From inside of `psql`, run `SELECT * FROM people;`
* From inside of `psql`, run `SELECT name FROM people;`
* From inside of `psql`, run `SELECT * FROM people WHERE age > 30;`

<h3 id="get-list-of-tables">How to get a list of tables?</h3>
* From inside of `psql`, run `\d`

<h3 id="get-columns-of-tables">How to get a columns from a table?</h3>
* From inside of `psql`, run `\d people`

<h3 id="add-a-new-column">How to get add column to an existing table?</h3>
* From inside of `psql`, run `ALTER TABLE people ADD COLUMN hair VARCHAR(50);`

<h3 id="total-number-of-entries">How to get a total number of entries in a table?</h3>
* From inside of `psql`, run `SELECT COUNT(*) FROM people;`
* From inside of `psql`, run `SELECT COUNT(*) FROM people WHERE age < 40;`

<h3 id="sum-of-values">How to sum the values in a single column?</h3>
* From inside of `psql`, run `SELECT SUM(age) FROM people;`

<h3 id="get-average-of-values">How to average the values in a single column?</h3>
* From inside of `psql`, run `SELECT AVG(age) FROM people;`

<h3 id="get-part-of-date-field">How to get part of a date/timestamp field?</h3>
* From inside of `psql`, run `SELECT date_part('unit', date(date_column)) FROM tablename;` <br>
    <p>'Unit' is a predefined abbreviation depending on what you are trying to display. See [9.9.1. EXTRACT, date_part](https://www.postgresql.org/docs/current/static/functions-datetime.html#FUNCTIONS-DATETIME-EXTRACT) for a list of possibilities. Some examples are: </p>
year - 4 digit representation of the year<br>
month - numerical representation of the month<br>
hour - numerical representation of the hour