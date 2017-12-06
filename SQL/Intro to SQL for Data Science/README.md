# Lesson - 1

* SQL, which stands for Structured Query Language, is a language for interacting with data stored in something called a relational database.
* You can think of a relational database as a collection of tables. A table is just a set of rows and columns, like a spreadsheet, which 	represents exactly one type of **entity**.
* For example, a table might represent employees in a company or purchases made, but not both.

* Each row, or record, of a table contains information about a single **entity**.
* For example, in a table representing employees, each row represents a single person. Each **column, or field**, of a table contains a single attribute for all rows in the table. 
* For example, in a table representing employees, we might have a column containing first and last names for all employees.


***

### Comments

```sql
-- Comments line
```

### Select a string to print 		
```sql
-- Try running me!
SELECT 'DataCamp <3 SQL'
AS result;
```

### Select a single column from a database

```sql
SELECT name FROM people;
```

### Select multiple columns from a database

```sql
SELECT name, birthdate
FROM people; 

-- all columns 
SELECT * 
FROM people;
```

### Select all the unique values from a column

```sql
SELECT DISTINCT language
FROM films;
```

### Count the number of rows in a table 

```sql
SELECT COUNT(*)
FROM people;

-- Count the number of non-missing values in a particular column
SELECT COUNT(birthdate)
FROM people;

-- Count unique birthdate 
SELECT COUNT(DISTINCT birthdate)
FROM people;

```



# Lesson - 2

## Filtering results

	In SQL, the WHERE keyword allows you to filter based on both text and numeric values in a table. There are a few different comparison operators you can use:

* = equal
* <> not equal
* < less than
* > greater than
* <= less than or equal to
* >= greater than or equal to

**Use <> and not != for the not equal operator, as per the SQL standard.**

Ex-

```
SELECT title 
FROM films
WHERE title = 'Metropolis';
```

```
SELECT title 
FROM films
WHERE release_year > 2000;
```