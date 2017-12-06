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

### Filtering results

	In SQL, the WHERE keyword allows you to filter based on both text and numeric values in a table. There are a few different comparison operators you can use:

### WHERE

* = equal
* <> not equal
* < less than
* > greater than
*  <= less than or equal to
*  >= greater than or equal to

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

### WHERE AND

```
SELECT title, release_year
FROM films
WHERE language='Spanish'
AND release_year < 2000;
```

```
SELECT title
FROM films
WHERE release_year > 1994 AND < 2000;
```

```
SELECT *
FROM films
WHERE language='Spanish'
AND release_year > 2000
AND release_year< 2010;
```


### WHERE AND OR


For example, the following returns all films released in either 1994 or 2000:

```
SELECT title
FROM films
WHERE release_year = 1994
OR release_year = 2000;
```

Note that you need to specify the column for every OR condition, so the following is invalid:

```
SELECT title
FROM films
WHERE release_year = 1994 OR 2000;
```

When combining AND and OR, be sure to enclose the individual clauses in parentheses, like so:

```
SELECT title
FROM films
WHERE (release_year = 1994 OR release_year = 1995)
AND (certification = 'PG' OR certification = 'R');
```
Otherwise, due to SQL's precedence rules, you may not get the results you're expecting!

Ex- 

```
SELECT title, release_year
FROM films
WHERE (release_year >= 1990 AND release_year <= 1999)
AND (language = 'French' OR language = 'Spanish')
AND (gross > 2000000)
```


### BETWEEN

```
SELECT title
FROM films
WHERE release_year >= 1994
AND release_year <= 2000;
```

Checking for ranges like this is very common, so in SQL the BETWEEN keyword provides a useful shorthand for filtering values within a specified range. This query is equivalent to the one above:

```
SELECT title
FROM films
WHERE release_year
BETWEEN 1994 AND 2000;
```

It's important to remember that BETWEEN is inclusive, meaning the beginning and end values are included in the results!

### WHERE IN

WHERE is very useful for filtering results. However, if you want to filter based on many conditions, WHERE can get unwieldy. For example:

```
SELECT name
FROM kids
WHERE age = 2
OR age = 4
OR age = 6
OR age = 8
OR age = 10;
```

Enter the IN operator! The IN operator allows you to specify multiple values in a WHERE clause, making it easier and quicker to specify multiple OR conditions! Neat, right?

So, the above example would become simply:

```
SELECT name
FROM kids
WHERE age IN (2, 4, 6, 8, 10);
```


### Introduction to NULL and IS NULL

In SQL, NULL represents a missing or unknown value. You can check for NULL values using the expression IS NULL. For example, to count the number of missing birth dates in the people table:

```
SELECT COUNT(*)
FROM people
WHERE birthdate IS NULL;
```

As you can see, IS NULL is useful when combined with WHERE to figure out what data you're missing.

Sometimes, you'll want to filter out missing values so you only get results which are not NULL. To do this, you can use the IS NOT NULL operator.

For example, this query gives the names of all people whose birth dates are not missing in the people table.

```
SELECT name
FROM people
WHERE birthdate IS NOT NULL;
```


### LIKE and NOT LIKE

In SQL, the LIKE operator can be used in a WHERE clause to search for a pattern in a column. To accomplish this, you use something called a wildcard as a placeholder for some other values. There are two wildcards you can use with LIKE:

The % wildcard will match zero, one, or many characters in text. For example, the following query matches companies like 'Data', 'DataC' 'DataCamp', 'DataMind', and so on:

```
SELECT name
FROM companies
WHERE name LIKE 'Data%';
```

The _ wildcard will match a single character. For example, the following query matches companies like 'DataCamp', 'DataComp', and so on:

```
SELECT name
FROM companies
WHERE name LIKE 'DataC_mp';
```

You can also use the NOT LIKE operator to find records that don't match the pattern you specify.

	Names of people whose names have 'r' as the second letter. The pattern you need is '_r%'.

```
SELECT name
FROM people
WHERE name LIKE '_r%';
```

```
SELECT name
FROM people
WHERE name NOT LIKE 'A%';
```


# Lesson - 3