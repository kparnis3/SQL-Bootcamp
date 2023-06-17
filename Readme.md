# Structured Query Language (SQL)

## SQL Example

-   We will learn how to write and use SQL
    -   SELECT customer_id, first_name, last_name
    -   FROM sales
    -   ORDER BY first_name;

# Section One: SQL Statement Fundamentals

## SELECT 

The most common statement used, it allows us to retrieve information about a table.

- Example syntax for SELECT statement:
    - SELECT column_name FROM table_name;
    - SELECT * FROM table_1; *selects all columns from table_1*
    - SELECT c1 FROM table_1; *selects c1 column from table_1*
    - SELECT c1,c2 FROM table_1; *selects c1,c2 columns from table_1*

## DISTINCT

Sometimes a table contains a column that had duplicate values, and you may find yourself in a situation where you only want to list the unique/distinct values.

The DISTINCT keyword can be used to return the only distinct value in a column.

- The DISTICT keyword operates on a column. The syntax looks like this:
    - SELECT DISTINCT column_name FROM table_name;
    - SELECT DISTINCT (column_name) FROM table_name; Add parenthesis for clarity

## COUNT

The COUNT function returns the number of input rows that match a specific condition of a query.

We can apply COUNT on a specific column or just pass COUNT(*), we will soon see this should return the same result.

Simply returns the number of rows in a table.

- Example syntax for SELECT statement:
    - SELECT COUNT(name) FROM table_name; returns BigInt
    - SELECT COUNT(DISTINCT name) FROM table_name; 

## SELECT WHERE

SELECT and WHERE are the most fundamental DQL statements we will find outselves using often.

The WHERE statement allows us to specify condisitons on columns for the rows to be returned.

- Example syntax for WHERE statement:
    -   SELECT column1, column2
        FROM table
        WHERE conditions;

The conditions are used to filter the rows returned from the SELECT statement.

- Comparison Operators
    - Comapre a column value to somethings.
        - Where is the price greater than $3.00?
        - Where is the pet's name equal to 'Sam'?

- Logical Operators
    - Allow us to combine multiple comparison operators.
        - AND
        - OR
        - NOT

- Simple syntax example:
    - SELECT name, choice FROM table WHERE name = 'David'; Returns rows from name column with name David.
    - SELECT name, choice FROM table WHERE name = 'David' AND choice='RED'; Returns rows from name column with name David aswell as choice Red.

## ORDER BY

PostgreSQL returns the same request query results in a different order.

We can use ORDER BY to sort rows based on a column value, in either ascending or descending order.

- Example syntax for ORDER BY:
    - SELECT column_1,column_2
      FROM table
      ORDER BY column_1 ASC/DESC

We can also ORDER BY muliple columns.

This makes sense when one column has duplicate entries.

- SELECT company,name,sales FROM table
  ORDER BY company, sales *Orders first by company and then by sales*

## LIMIT

The LIMIT keyword allows us to limit the number of rows returned for a query.

This is useful for not wanting to return every single row in a table, but only view the top few rows to get an idea of the table layout.

LIMIT is also useful in combination with ORDER BY.

LIMIT goes at the very end of a query request and is the last command to be executed.

## BETWEEN

The BETWEEN operator can be used to match a value against a range of values:
- WHERE value BETWEEN low AND high

The BETWEEN operator is the same as:
- value >= low AND calue <= high
- WHERE value BETWEEN low AND high

We can also combine BETWEEN with the NOT logical operator:
- WHERE value NOT BETWEEN low AND high

The NOT BETWEEN operator is the same as:
- WHERE value < low OR value > high
- WHERE value NOT BETWEEN low AND high

The BETWEEN operator can also be used with dates. Not that you need to format dates in the ISO 8601 standard format, which is YYYY-MM-DD
-   WHERE date BETWEEN '2007-01-01' AND '2007-02-01'

## IN

Certain cases we want to check for multiple possible value options, for example, if a user's name shows up IN a list of known names.

We can use the IN operator to create a condition that checks to see if a value is included in a list of multiple options.

- The general syntax is:
    - value IN (option1,option2,...,option_n);

- Example query:   
    - SELECT color FROM table WHERE color in ('red','blue','green');
    - SELECT color FROM table WHERE color NOT in ('red','blue');

## LIKE and ILIKE

Used when we want to match against a general pattern in a string.
- All emails ending in '@gmail.com'
- All names that begin with an 'A'

The LIKE operator allows us to perform pattern matching agaianst string data with wildcard characters:
- Percent %
    - Matches any sequence of characters.
- Underscore _
    - Matches any single character.

- All names that begin with an 'A'
    - WHERE name LIKE 'A%'

- All names that end with an 'a'
    - WHERE name LIKE '%a'

Notice that LIKE is case-sensitive, we can use ILIKE which is case-insensitive.

Using the underscore allows us to replace just a single character.
- Get all Mission Impossible Films
- WHERE title LIKE 'Mission Impossible _'

We can use multiple underscores

Imagine we had version string codes in the format 'Version#A4', 'Version#B7', etc..
- WHERE value LIKE 'Version#__'

We can also combine pattern matching operators to create more complex patterns.
- WHERE name LIKE '_her%'
    - Cheryl
    - Theresa
    - Sherri

# Section Two: GROUP BY Statements

GROUP BY will allow us to aggregate data and apply funcations to better understand how data is distributed per category.

## Aggregate Functions

The main idea behind an aggregate function is to take multiple inputs and return a single output.

The most common aggregate functions:

- AVG() - returns average value.
- COUNT() - returns number of values.
- MAX() - returns maximum value.
- MIN() - returns minimum value.
- SUM() - returns the sum of all values.

Aggregate functions calls happen only in the SELECT clause or the HAVING clause.

- Special Notes
    - AVG() returns a floating point value many decimal places (e.g. 2.342418..)
        - We can use ROUND() to specify precision after the decimal.

    - COUNT() simply returns  the number of rows, which simply means by convention we just use COUNT(*).

## GROUP BY

Allows us to aggregate columns per some category.

- Example syntax for GROUP BY:
    - SELECT category_col, AGG(data_col)
      FROM table
      WHERE category_col!='A'
      GROUP BY category_col
    
The GROUP BY clause must appear right after a FROM or WHERE statement.

In the SELECT statement, columns must either have an aggregate function or be in the GROUP BY call.

WHERE statements should not refer to the aggregation result, later on we will learn to use HAVING to filter those results.

If we want to sort the result based on the aggregate, we need to make sure to reference the entire function.

- Example:
    - SELECT company, SUM(sales) 
      FROM finance_table
      GROUP BY company
      ORDER BY SUM(sales)

## HAVING

We can't use WHERE to filter based off of aggregate results, because those happen after a WHERE is executed.

- SELECT comapny, SUM(sales)
  FROM finance_table
  WHERE company!='Google'
  GROUP BY company
  HAVING SUM(sales) > 1000

Having allows us to use the aggregate result as a filter along with a GROUP BY.



