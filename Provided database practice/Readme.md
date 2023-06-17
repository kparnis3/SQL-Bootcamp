Viewing Tables in Postgre:

Databases -> [DATABASE NAME] -> Schemas -> public -> Tables

# Section One: SQL Statement Fundamentals

## Statements used: SELECT

SELECT * FROM actor;

SELECT first_name FROM actor;

SELECT first_name,last_name FROM actor;

## Challenge One

-   Situation
    -   We want to send out a promotional email to our existing customers!
    -   Use a SELECT statement to grab the first and last names of every customer and their email  address.

Answer: <br>
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

Answer: <br>
SELECT DISTINCT rating FROM film;

## Statements used: COUNT

SELECT COUNT(*) *FROM payment; returns 14596*

SELECT COUNT(amount) *FROM payment; returns 14596*

### How distinct amounts payed?

SELECT COUNT(DISTINCT amount) FROM payment; 

## Statements used: WHERE

SELECT * FROM customer <br>
WHERE first_name='Jared';

SELECT * FROM film <br>
WHERE rental_rate > 4 AND replacement_cost >= 19.99;

### List movies that fit the three conditions

SELECT title FROM film <br>
where rental_rate > 4 AND replacement_cost >= 19.99 <br>
and rating='R';

### How many movies fit the three conditions?

SELECT count(*) FROM film    <br>
where rental_rate > 4 AND replacement_cost >= 19.99 <br>
and rating='R'; 

### How many movies fit are R rated or PG-13 rated?

SELECT COUNT(*) FROM film <br>
WHERE rating = 'R' OR rating = 'PG-13'; 

### List movies that are R rated

SELECT * FROM film <br>
WHERE rating != 'R'; 

## Challenge Three

From now on more buisness related questions are asked.

- Situtation One
    - A customer forgot their wallet at our store! We need to track down their email to inform them.
    - What is the email for the customer with the name Nancy Thomas

Answer: <br>
SELECT email FROM customer <br>
WHERE first_name='Nancy' AND last_name='Thomas';

- Situtation Two
    - A customer wants to know what movie 'Outlaw Hanky' is about.
    - Could you give them the description for the movie 'Outlaw Hanky';

Answer: <br>
SELECT title,description FROM film <br>
WHERE title='Outlaw Hanky';

- Situtation Three
    - A customer is late on their  movie return, and we've mailed them a letter to their address at '259 Ipoh Drive'. We should also call them on the phone to let them know.
    - Can you get the phone number for the customer who lives at '259 Ipoh Drive'?

Answer: <br>
SELECT phone FROM address <br>
WHERE address='259 Ipoh Drive';

## Statements used: ORDER BY

### Orders everything in descending order

SELECT * FROM customer <br>
ORDER BY first_name DESC; 

### Orders first by id and then by name in ascending order

SELECT store_id,first_name,last_name FROM customer <br>
ORDER BY store_id,first_name ASC; 

### Orders first by id in decending order and then by name in decending order

SELECT store_id,first_name,last_name FROM customer <br>
ORDER BY store_id DESC,first_name ASC;

## Statements used: LIMIT

### Get the top two most oldest transaction

SELECT * FROM payment <br>
ORDER BY payment_date ASC <br>
LIMIT 2;

### Get the top five most recent payments which amounts weren't zero

SELECT * FROM payment <br>
WHERE amount != 0 <br>
ORDER BY payment_date DESC <br>
LIMIT 5;

### Get Table's first rows

SELECT * FROM payment <br>
LIMIT 1;

## Challenge Four
- Situtation One
    - We want to reward our first 10 paying customers.
    - What are the customer ids of the first 10 customers who created a payment?

Answer:<br>
SELECT customer_id FROM payment <br>
ORDER BY payment_date ASC <br>
LIMIT 10; 

- Situation Two
    - A customer wants to quickly rent a video to watch over their short lunch break.
    - What are the titles of the five shortest (in length) movies?

Answer: <br>
SELECT title,length FROM film <br>
ORDER BY length ASC <br>
LIMIT 5;

- Situation Three
    - If a customer can watch any movie that is 50min or less in run time, how many options do they have?

Answer: <br>
SELECT COUNT(title) FROM film <br>
WHERE length <= 50;

## Statements used: BETWEEN

### Get all columns that are between 8$ to 9$*

SELECT * FROM payment <br>
WHERE amount BETWEEN 8 AND 9;

### Count how many transactions are between 8$ ansd 9$

SELECT COUNT(*) FROM payment <br>
WHERE amount BETWEEN 8 AND 9;

### Count how many transactions aren't between 8$ and 9$

SELECT COUNT(*) FROM payment <br>
WHERE amount NOT BETWEEN 8 AND 9; 

### Get all columns between transaction dates

SELECT * FROM payment <br>
WHERE payment_date BETWEEN '2007-02-01' AND '2007-02-15';

## Statements used: IN

### All rows that have payments that are either 0.99, 1.99 or 7.99

SELECT * FROM payment <br>
WHERE amount in(0.99,1.99,7.99) <br>
ORDER BY amount;

### How many payments are either 0.99, 1.99 or 7.99?

SELECT COUNT(*) FROM payment  <br>
WHERE amount in(0.99,1.99,7.99); 

### Are there customers called john, jake or julie

SELECT * FROM customer <br>
WHERE first_name in('John','Jake','Julie'); 

## Statements used: LIKE and ILIKE

### Get the amount of names that start with the letter J

SELECT COUNT(*) FROM customer <br>
WHERE first_name LIKE  'J%';

### List all the names and surnames that start with J for name and S for surname

SELECT first_name,last_name FROM customer <br>
WHERE first_name LIKE  'J%' AND last_name LIKE 'S%'; 

### Ignoring case sensitivity

SELECT first_name,last_name FROM customer <br>
WHERE first_name ILIKE  'j%' AND last_name ILIKE 's%'; 

### List all customers that start with any single character followed by her and any amount of characters

SELECT * FROM customer <br>
WHERE first_name ILIKE  '_her%';

### List all customers that Start with A and are ordered by there last names

SELECT * FROM customer <br>
WHERE first_name LIKE 'A%' <br>
ORDER BY last_name;

## General Challenge

These challenges utilize all the skills learned so far!

- Situation One
    - How many payment trasnsactions were greater than $5.00?

Answer: <br>
SELECT COUNT(*) FROM payment <br>
WHERE amount > 5;

- Situation Two
    - How many actors have a first name that starts with the letter P?

Answer: <br>
SELECT COUNT(*) FROM actor <br>
WHERE first_name LIKE 'P%';

- Situation Three
    - How many unique districts are our customers from?

Answer:
SELECT COUNT(DISTINCT district) FROM address;

- Situation Four
    - Retrieve the list of names for those distinct districts from the previous question.

Answer: <br>
SELECT DISTINCT(district) FROM address;

- Situation Five
    - How many films have a rating of R and a replacement cost between $5 and $15?

Answer: <br>
SELECT COUNT(*) FROM film <br>
WHERE rating = 'R' <br>
AND replacement_cost BETWEEN 5 AND 15;

- Situation Six
    - How many films have the word Truman somewhere in the title?

Answer: <br>
SELECT COUNT(*) FROM film <br>
WHERE title LIKE '%Truman%';

# Section Two: GROUP BY Statements

## Aggregate Functions

### Whats the minimum replacement cost for a film?

SELECT MIN(replacement_cost) FROM film;

### Whats the maximum replacement cost for a film?

SELECT MAX(replacement_cost) FROM film;

### What are the minimum and maximum replacement costs for a film?

SELECT MAX(replacement_cost), MIN(replacement_cost) FROM film;

### Whats the average replacement cost for a film in 2 decimal places?

SELECT ROUND(AVG(replacement_cost), 2) <br>
FROM film;

### Whats the sum of all replacement costs for films?

SELECT SUM(replacement_cost) FROM film;

## GROUP BY

### What are the distinct customer ids? 

SELECT customer_id FROM payment <br>
GROUP BY customer_id;

### What are the customer id's sum amount in descending order? 

SELECT customer_id, SUM(amount) FROM payment <br>
GROUP BY customer_id <br>
ORDER BY SUM(amount) DESC;

### Whats the total spent by a customer with staff?

SELECT customer_id, staff_id, SUM(amount) FROM payment <br>
GROUP BY staff_id, customer_id <br>
ORDER BY customer_id;

### How much money are we making every day?

SELECT DATE(payment_date), SUM(amount) FROM payment <br>
GROUP BY DATE(payment_date) <br>
ORDER by DATE(payment_date) ASC;

## Challenge Five
- Situtation One
    - We have two staff members, with Staff IDs 1 and 2. We want to give a bonus to the staff member that handled the most payments.
    (Most in terms of number if payments processed, not total dollar amount).
    - How many payments did each staff meber handle and who gets the bonus?

Answer: <br>
SELECT staff_id, COUNT(amount) <br>
FROM payment <br>
GROUP BY staff_id <br>
ORDER BY SUM(amount) DESC;

- Situtation Two
    - Corporate HQ is conducting a study on the relationship between replacement cost and a movie MPAA rating (e.g G, PG, R, etc...)
    - What is the average replacement cost per MPAA rating?

Answer: <br>
SELECT rating, ROUND(AVG(replacement_cost), 2) <br>
FROM film <br>
GROUP BY rating <br>
ORDER BY AVG(replacement_cost) DESC;

- Situtation Three
    - We are running a promotion to reward our top 5 customers with coupons.
    - What are the customer_ids of the top 5 customers by total spent?

SELECT customer_id, SUM(amount) <br>
FROM payment <br>
GROUP BY customer_id <br>
ORDER BY SUM(amount) DESC <br>
LIMIT 5;

## HAVING

### Whats the sum spend by a customer id  which is over 100?

SELECT customer_id, SUM(amount) FROM payment <br>
GROUP BY customer_id <br>
HAVING SUM(AMOUNT) > 100 <br>
ORDER BY SUM(AMOUNT);

### How many customers are there in each store over 300?

SELECT store_id, COUNT(customer_id) FROM customer <br>
GROUP BY store_id <br>
HAVING COUNT(customer_id) > 300;

## Challenge Six

- Situtation One
    - We are launching a platinum service for our most loyal customers. We will assign platinum status to customers that have had 40 or more transaction payments.
    - What customer_ids are eligible for platinum status?

Answer: <br>
SELECT customer_id, COUNT(amount) FROM payment <br>
GROUP BY customer_id <br>
HAVING COUNT(amount) >= 40; <br>


- Situtation Two
    - What are the customer_ids of customers who have spent more than 100$ in payment transactions with our staff_ids memebr 2?

Answer: <br>
SELECT customer_id, SUM(amount) FROM payment <br>
WHERE staff_id=2 <br>
GROUP BY customer_id <br>
HAVING SUM(amount) > 100;

# Assesment Test 1

- Question One
    - Return the customer IDs of customers who have spent at least $110 with the staff member who has an ID of 2.

Answer:<br>
SELECT customer_id, SUM(amount) FROM payment <br>
WHERE staff_id=2 <br>
GROUP BY customer_id <br>
HAVING SUM(amount) >= 110;

- Question Two
    - How many films begin with the letter J?

Answer:<br>
SELECT COUNT(*) FROM film <br>
WHERE title LIKE 'J%';

- Question Three
    - What customer has the highest customer ID number whose name starts with an 'E' and has an address ID lower than 500?

Answer:<br>
SELECT first_name,last_name FROM customer<br>
WHERE first_name LIKE 'E%' AND address_id < 500<br>
ORDER BY customer_id DESC<br>
LIMIT 1;

 
