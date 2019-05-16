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

```
* = equal
* <> not equal
* < less than
* > greater than
*  <= less than or equal to
*  >= greater than or equal to
```
**Use <> and not != for the not equal operator, as per the SQL standard.**

Ex-

```sql
SELECT title 
FROM films
WHERE title = 'Metropolis';
```

```sql
SELECT title 
FROM films
WHERE release_year > 2000;
```

### WHERE AND

```sql
SELECT title, release_year
FROM films
WHERE language='Spanish'
AND release_year < 2000;
```

```sql
SELECT title
FROM films
WHERE release_year > 1994 AND < 2000;
```

```sql
SELECT *
FROM films
WHERE language='Spanish'
AND release_year > 2000
AND release_year< 2010;
```


### WHERE AND OR


For example, the following returns all films released in either 1994 or 2000:

```sql
SELECT title
FROM films
WHERE release_year = 1994
OR release_year = 2000;
```

Note that you need to specify the column for every OR condition, so the following is invalid:

```sql
SELECT title
FROM films
WHERE release_year = 1994 OR 2000;
```

When combining AND and OR, be sure to enclose the individual clauses in parentheses, like so:

```sql
SELECT title
FROM films
WHERE (release_year = 1994 OR release_year = 1995)
AND (certification = 'PG' OR certification = 'R');
```
Otherwise, due to SQL's precedence rules, you may not get the results you're expecting!

Ex- 

```sql
SELECT title, release_year
FROM films
WHERE (release_year >= 1990 AND release_year <= 1999)
AND (language = 'French' OR language = 'Spanish')
AND (gross > 2000000)
```


### BETWEEN

```sql
SELECT title
FROM films
WHERE release_year >= 1994
AND release_year <= 2000;
```

Checking for ranges like this is very common, so in SQL the BETWEEN keyword provides a useful shorthand for filtering values within a specified range. This query is equivalent to the one above:

```sql
SELECT title
FROM films
WHERE release_year
BETWEEN 1994 AND 2000;
```

It's important to remember that BETWEEN is inclusive, meaning the beginning and end values are included in the results!

### WHERE IN

WHERE is very useful for filtering results. However, if you want to filter based on many conditions, WHERE can get unwieldy. For example:

```sql
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

```sql
SELECT name
FROM kids
WHERE age IN (2, 4, 6, 8, 10);
```


### Introduction to NULL and IS NULL

In SQL, NULL represents a missing or unknown value. You can check for NULL values using the expression IS NULL. For example, to count the number of missing birth dates in the people table:

```sql
SELECT COUNT(*)
FROM people
WHERE birthdate IS NULL;
```

As you can see, IS NULL is useful when combined with WHERE to figure out what data you're missing.

Sometimes, you'll want to filter out missing values so you only get results which are not NULL. To do this, you can use the IS NOT NULL operator.

For example, this query gives the names of all people whose birth dates are not missing in the people table.

```sql
SELECT name
FROM people
WHERE birthdate IS NOT NULL;
```


### LIKE and NOT LIKE

In SQL, the LIKE operator can be used in a WHERE clause to search for a pattern in a column. To accomplish this, you use something called a wildcard as a placeholder for some other values. There are two wildcards you can use with LIKE:

The % wildcard will match zero, one, or many characters in text. For example, the following query matches companies like 'Data', 'DataC' 'DataCamp', 'DataMind', and so on:

```sql
SELECT name
FROM companies
WHERE name LIKE 'Data%';
```

The _ wildcard will match a single character. For example, the following query matches companies like 'DataCamp', 'DataComp', and so on:

```sql
SELECT name
FROM companies
WHERE name LIKE 'DataC_mp';
```

You can also use the NOT LIKE operator to find records that don't match the pattern you specify.

	Names of people whose names have 'r' as the second letter. The pattern you need is '_r%'.

```sql
SELECT name
FROM people
WHERE name LIKE '_r%';
```

```sql
SELECT name
FROM people
WHERE name NOT LIKE 'A%';
```


# Lesson - 3

### Aggregate functions

For example,

```sql
SELECT AVG(budget)
FROM films;
```

gives you the average value from the budget column of the films table. Similarly, the MAX function returns the highest budget:

```sql
SELECT MAX(budget)
FROM films;
```

The SUM function returns the result of adding up the numeric values in a column:

```sql
SELECT SUM(budget)
FROM films;
```

You can probably guess what the MIN function does! Now it's your turn to try out some SQL functions.

### Combining aggregate functions with WHERE

```sql
SELECT SUM(budget)
FROM films
WHERE release_year >= 2010;
```

### A note on arithmetic

In addition to using aggregate functions, you can perform basic arithmetic with symbols like + , -, * , and / .

So, for example, this gives a result of 12:

```
SELECT (4 * 3);
```

However, the following gives a result of 1:

```sql
SELECT (4 / 3);
```

What's going on here?

SQL assumes that if you divide an integer by an integer, you want to get an integer back. So be careful when dividing!

If you want more precision when dividing, you can add decimal places to your numbers. For example,

```sql
SELECT (4.0 / 3.0) AS result;
```

gives you the result you would expect: 1.333.


### It's AS simple AS aliasing

 SQL allows you to do something called aliasing. Aliasing simply means you assign a temporary name to something. To alias, you use the AS keyword, which you've already seen earlier in this course.

For example, in the above example we could use aliases to make the result clearer:

```sql
SELECT MAX(budget) AS max_budget,
       MAX(duration) AS max_duration
FROM films;
```


# Lesson - 4

### ORDER BY 

In SQL, the **ORDER BY** keyword is used to sort results in ascending or descending order according to the values of one or more columns.

By default ORDER BY will sort in ascending order. If you want to sort the results in descending order, you can use the DESC keyword. For example,

```sql
SELECT title
FROM films
ORDER BY release_year DESC;
```
gives you the titles of films sorted by release year, from newest to oldest.


```sql
SELECT title, gross
FROM films  
--WHERE release_year NOT IN (2015)
WHERE title LIKE 'M%'
ORDER BY release_year;
```


### Sorting single columns (DESC)

```sql
SELECT imdb_score
FROM reviews
ORDER BY imdb_score DESC
```

### Sorting multiple columns

ORDER BY can also be used to sort on multiple columns. It will sort by the first column specified, then sort by the next, then the next, and so on. For example,

```sql
SELECT birthdate, name
FROM people
ORDER BY birthdate, name;
```


### GROUP BY

In SQL, GROUP BY allows you to group a result by one or more columns, like so:

```sql
SELECT sex, count(*)
FROM employees
GROUP BY sex;
```

Commonly, **GROUP BY** is used with aggregate functions like **COUNT()** or **MAX()**. Note that **GROUP BY** always goes after the **FROM** clause!

A word of warning: SQL will return an error if you try to SELECT a field that is not in your GROUP BY clause without using it to calculate some kind of value about the entire group.

Note that you can combine GROUP BY with ORDER BY to group your results, calculate something about them, and then order your results. For example,

```sql
SELECT sex, count(*)
FROM employees
GROUP BY sex
ORDER BY count DESC;
```

Get the release year and average duration of all films, grouped by release year.

```sql
SELECT release_year, AVG(duration)
FROM films
GROUP BY release_year
```


Get the language and total gross amount films in each language made.

```sql
SELECT language, SUM(gross)
FROM films
GROUP BY language;
```

Get the release year, country, and highest budget spent making a film for each year, for each country. Sort your results by release year and country.

```sql
SELECT release_year, country, MAX(budget)
FROM films
GROUP BY release_year, country
ORDER BY release_year, country;
```

HAVING a great time
In SQL, aggregate functions can't be used in WHERE clauses. For example, the following query is invalid:

```sql
SELECT release_year
FROM films
GROUP BY release_year
WHERE COUNT(title) > 10;
```
This means that if you want to filter based on the result of an aggregate function, you need another way! That's where the HAVING clause comes in. For example,

```sql
SELECT release_year
FROM films
GROUP BY release_year
HAVING COUNT(title) > 10;
```

Now you're going to write a query that returns the average budget and average gross earnings for films in each year after 1990, if the average budget is greater than $60 million.

```sql
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990 
GROUP BY release_year
HAVING  AVG(budget) > 60000000
ORDER BY avg_gross DESC;
```

Get the country, average budget, and average gross take of countries that have made more than 10 films. Order the result by country name, and limit the number of results displayed to 5. You should alias the averages as avg_budget and avg_gross respectively.

```sql
-- select country, average budget, average gross
SELECT country,AVG(budget) as avg_budget, AVG(gross) as avg_gross
-- from the films table
FROM films
-- group by country 
GROUP BY country
-- where the country has a title count greater than 10
HAVING COUNT(title) > 10
-- order by country
ORDER BY country
-- limit to only show 5 results
LIMIT 5 
```

Other query

```sql
SELECT title, imdb_score
FROM films
JOIN reviews
ON films.id = reviews.film_id
WHERE title = 'To Kill a Mockingbird';
```