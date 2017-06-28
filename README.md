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

* [How do I generate a project with knex built in?](#generate-knex-project)
* [How do I create a migration file for knex?](#create-migration-file)
* [How do I create a table with the migration file?](#create-migration-file)
* [How do I create a seed file for knex?](#create-seed-file)
* [How do I add data to a seed file using knex?](#add-data-to-seed-file)
* [How to return all data from GET API route?](#return-all-data)
* [How to add data with POST API route?](#add-data)

<a id="how-to-start-psql"></a>
### How to start PSQL?
* Open terminal window
* Type `psql postgres` OR `psql name-of-db`

<a id="how-to-create-db"></a>
### How to create a database?
* From inside of `psql`, run `CREATE DATABASE testdb`
* Alternate option would be to run `createdb testdb` from the terminal.

<a id="connect-to-db"></a>
### How to connect to a database?
* From inside of `psql`, run `\c testdb`

<a id="create-a-table"></a>
### How to create a table?
* From inside of `psql`, run `CREATE TABLE people(id SERIAL, name VARCHAR(255), age INT);`

<a id="insert-data-into-table"></a>
### How to insert data into table?
* From inside of `psql`, run `INSERT INTO people VALUES(DEFAULT, 'james', 44);`
* From inside of `psql`, run `INSERT INTO people(name, age) VALUES('james', 44);`

<a id="update-data-inside-table"></a>
### How to update data inside table?
* From inside of `psql`, run `UPDATE people SET age = 33 WHERE name = 'james';`

<a id="delete-data-from-table"></a>
### How to delete data from table?
* From inside of `psql`, run `DELETE FROM people WHERE name = 'james';`

<a id="query-data-from-table"></a>
### How to query data from table?
* From inside of `psql`, run `SELECT * FROM people;`
* From inside of `psql`, run `SELECT name FROM people;`
* From inside of `psql`, run `SELECT * FROM people WHERE age > 30;`

<a id="get-list-of-tables"></a>
### How to get a list of tables?
* From inside of `psql`, run `\d`

<a id="get-columns-of-tables"></a>
### How to get a columns from a table?
* From inside of `psql`, run `\d people`

<a id="add-a-new-column"></a>
### How to get add column to an existing table?
* From inside of `psql`, run `ALTER TABLE people ADD COLUMN hair VARCHAR(50);`

<a id="total-number-of-entries"></a>
### How to get a total number of entries in a table?
* From inside of `psql`, run `SELECT COUNT(*) FROM people;`
* From inside of `psql`, run `SELECT COUNT(*) FROM people WHERE age < 40;`

<a id="sum-of-values"></a>
### How to sum the values in a single column?
* From inside of `psql`, run `SELECT SUM(age) FROM people;`

<a id="get-average-of-values"></a>
### How to average the values in a single column?
* From inside of `psql`, run `SELECT AVG(age) FROM people;`


## Knex

<a id="generate-knex-project"></a>
### How do I generate a project with knex built in?
* From inside of the terminal, run `dbconfig knex scaffold --dbname=people --create-dir=somefoldername`
* `cd` into child directory you just created
* Run `createdb somedb`
* Run `npm install`

<a id="create-migration-file"></a>
### How do I create a migration file for knex?
* From inside of the terminal, run `knex migrate:make create_people_table`

<a id="create-a-table"></a>
### How do I create a table with the migration file?
* From inside of the `create_people_table` migration file, add columns. Example:
```
exports.up = function(knex, Promise) {
  return knex.schema.createTable('people', function(table) {
    table.increments();
    table.string('name').notNullable();
    table.integer('age');
    table.string('email').notNullable();
    table.timestamps(true, true);
  });
};

exports.down = function(knex, Promise) {
  return knex.schema.createTable('people');
};
```

<a id="create-seed-file"></a>
### How do I create a seed file for knex?
* From inside of the terminal, run `knex seed:make people_seed_file`

<a id="add-data-to-seed-file"></a>
### How do I add data to a seed file using knex?
* From inside of the seed file, add the dummy data. Example:
```
exports.seed = function(knex, Promise) {
  // Deletes ALL existing entries
  return knex('people').del()
    .then(function () {
      // Inserts seed entries
      return knex('people').insert([
        {name: 'james taylor', age: 22, email: 'j@t.com'},
        {name: 'john daly', age: 29, email: 'j@d.com'},
        {name: 'jimmy buffett', age: 44, email: 'j@b.com'},
      ]);
    });
};

```

<a id="return-all-data"></a>
### How to return all data from GET API route?
* Inside of the routes file, add the following:
```
app.get('/people', function(req, res) {
  knex.raw(`select * from people`).then(function(people) {
    res.send(people.rows);
  });
});
```

<a id="add-data"></a>
### How to add data with POST API route?
* Inside of the routes file, add the following:
```
app.post('/people', function(req, res) {
  knex.raw(`insert into people(name, age, email) values('${req.body.name}', ${req.body.age}, '${req.body.email}')`).then(function() {
    knex.raw(`select * from people`).then(function(people) {
      res.send(people.rows);
    });
  })
})
```
