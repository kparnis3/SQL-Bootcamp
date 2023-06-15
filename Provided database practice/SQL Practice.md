Viewing Tables in Postgre:

Databases -> [DATABASE NAME] -> Schemas -> public -> Tables

## Statements used: SELECT

SELECT * FROM actor;

SELECT first_name FROM actor;

SELECT first_name,last_name FROM actor;

## Challenge One

-   Situation
    -   We want to send out a promotional email to our existing customers!
    -   Use a SELECT statement to grab the first and last names of every customer and their email  address.

Answer: 
SELECT first_name,last_name,email FROM customer;

## Statements used: DISTINCT

SELECT DISTINCT release_year FROM film;

SELECT DISTINCT (release_year) FROM film;

SELECT DISTINCT (rental_rate) FROM film;

## Challenge Two

- Situtation
    -   An Australian visitor isn't familiar with MPAA movie ratings (eg: PG, PG-13, R, etc..)
    -   We want to know the types of ratings we have in our db.
    -   What ratings do we have?

Answer: 
SELECT DISTINCT rating FROM film;

## Statements used: COUNT

SELECT COUNT(*) *FROM payment; returns 14596*

SELECT COUNT(amount) *FROM payment; returns 14596*

SELECT COUNT(DISTINCT amount) FROM payment; *returns 19, How distinct amounts payed?*

## Statements used: WHERE

SELECT * FROM customer
WHERE first_name='Jared';

SELECT * FROM film
where rental_rate > 4 AND replacement_cost >= 19.99;

SELECT title FROM film
where rental_rate > 4 AND replacement_cost >= 19.99
and rating='R'; *List movies fit the three conditions?*

SELECT count(*) FROM film    
where rental_rate > 4 AND replacement_cost >= 19.99
and rating='R'; *How many movies fit the three conditions?*

SELECT COUNT(*) FROM film
WHERE rating = 'R' OR rating = 'PG-13'; *How many movies fit are R rated or PG-13 rated*

SELECT * FROM film
WHERE rating != 'R'; *List movies that are R rated*

## Challenge Three

From now on more buisness related questions are asked.

- Situtation One
    - A customer forgot their wallet at our store! We need to track down their email to inform them.
    - What is the email for the customer with the name Nancy Thomas

Answer: 
SELECT email FROM customer
WHERE first_name='Nancy' AND last_name='Thomas';

- Situtation Two
    - A customer wants to know what movie 'Outlaw Hanky' is about.
    - Could you give them the description for the movie 'Outlaw Hanky';

Answer: 
SELECT title,description FROM film
WHERE title='Outlaw Hanky';


- Situtation Three
    - A customer is late on their  movie return, and we've mailed them a letter to their address at '259 Ipoh Drive'. We should also call them on the phone to let them know.
    - Can you get the phone number for the customer who lives at '259 Ipoh Drive'?

Answer: 
SELECT phone FROM address
WHERE address='259 Ipoh Drive';

## Statements used: ORDER BY

SELECT * FROM customer 
ORDER BY first_name DESC; *Orders everything in descending order*

SELECT store_id,first_name,last_name FROM customer
ORDER BY store_id,first_name ASC; *Orders first by id and then by name in ascending order*

SELECT store_id,first_name,last_name FROM customer
ORDER BY store_id DESC,first_name ASC; *Orders first by id in decending order and then by name in decending order*

## Statements used: LIMIT

SELECT * FROM payment
ORDER BY payment_date ASC
LIMIT 2; *Get the top two most oldest transaction*

SELECT * FROM payment
WHERE amount != 0
ORDER BY payment_date DESC
LIMIT 5; *Get the top five most recent payments which amounts weren't zero*

SELECT * FROM payment
LIMIT 1; *Get Table's first rows*

## Challenge Three

- Situtation One
    - We want to reward our first 10 paying customers.
    - What are the customer ids of the first 10 customers who created a payment?

Answer:
SELECT customer_id FROM payment
ORDER BY payment_date ASC
LIMIT 10;

- Situation Two
    - A customer wants to quickly rent a video to watch over their short lunch break.
    - What are the titles of the five shortest (in length) movies?

Answer:
SELECT title,length FROM film
ORDER BY length ASC
LIMIT 5;

- Situation Three
    - If a customer can watch any movie that is 50min or less in run time, how many options do they have?

Answer:
SELECT COUNT(title) FROM film
WHERE length <= 50;

## Statements used: BETWEEN

SELECT * FROM payment
WHERE amount BETWEEN 8 AND 9; *Get all columns that are between 8$ to 9$*

SELECT COUNT(*) FROM payment
WHERE amount BETWEEN 8 AND 9; *count how many transactions are between 8$ ansd 9$*

SELECT COUNT(*) FROM payment
WHERE amount NOT BETWEEN 8 AND 9; *count how many transactions aren't between 8$ and 9$*

SELECT * FROM payment
WHERE payment_date BETWEEN '2007-02-01' AND '2007-02-15'; *Get all columns between transaction dates*

## Statements used: IN

SELECT * FROM payment
WHERE amount in(0.99,1.99,7.99)
ORDER BY amount; *All rows that have payments that are either 0.99, 1.99 or 7.99*

SELECT COUNT(*) FROM payment 
WHERE amount in(0.99,1.99,7.99); *How many payments are either 0.99, 1.99 or 7.99?*

SELECT * FROM customer
WHERE first_name in('John','Jake','Julie');  *Are there customers called john, jake or julie*

## Statements used: LIKE and ILIKE

SELECT COUNT(*) FROM customer
WHERE first_name LIKE  'J%'; *Get the amount of names that start with the letter J*

SELECT first_name,last_name FROM customer
WHERE first_name LIKE  'J%' AND last_name LIKE 'S%'; *List all the names and surnames that start with J for name and S for surname*

SELECT first_name,last_name FROM customer
WHERE first_name ILIKE  'j%' AND last_name ILIKE 's%'; *Ignoring case sensitivity*

SELECT * FROM customer
WHERE first_name ILIKE  '_her%'; *List all customers that start with any single character followed by her and any amount of characters*

SELECT * FROM customer
WHERE first_name LIKE 'A%'
ORDER BY last_name; *List all customers that Start with A and are ordered by there last names*

## General Challenge

These challenges utilize all the skills learned so far!

- Situation One
    - How many payment trasnsactions were greater than $5.00?

Answer:
SELECT COUNT(*) FROM payment
WHERE amount > 5;

- Situation Two
    - How many actors have a first name that starts with the letter P?

Answer:
SELECT COUNT(*) FROM actor
WHERE first_name LIKE 'P%';

- Situation Three
    - How many unique districts are our customers from?

Answer:
SELECT COUNT(DISTINCT district) FROM address;

- Situation Four
    - Retrieve the list of names for those distinct districts from the previous question.

Answer:
SELECT DISTINCT(district) FROM address;

- Situation Five
    - How many films have a rating of R and a replacement cost between $5 and $15?

Answer:
SELECT COUNT(*) FROM film
WHERE rating = 'R'
AND replacement_cost BETWEEN 5 AND 15;

- Situation Six
    - How many films have the word Truman somewhere in the title?

Answer:

SELECT COUNT(*) FROM film
WHERE title LIKE '%Truman%';