# Soluciones a las Prácticas de DataLemur
### Lección 102
#### Práctica 1 - SQL Select Practice Exercise
Your given a products table, which contains data about different Microsoft Azure cloud products.
Output all the data, in all the columns
CODIGO : 
SELECT * FROM products;
### Lección 103
#### Práctica 2 - WHERE Practice Exercise
Given the reviews table, write a query to retrieve all 3-star reviews using the SQL WHERE clause.
Only display the user_id and stars columns
CODIGO :
SELECT user_id,stars FROM reviews WHERE stars=3;
### Lección 104
#### Práctica 3 - SQL WHERE AND Practice Exercise
the review should have 4 or more stars
the review ID is less than 6000
the review ID is more than 2000
the review can't come from user 142
CODIGO :
SELECT * FROM reviews WHERE stars > 3 
  AND review_id < 6000
  AND review_id >2000
  AND user_id != 142;
#### Práctica 4 - SQL AND OR Practice Exercise
Let's practice using AND along with WHERE to filter Amazon reviews based on these two conditions:
the start count is greater than 2, and less than or equal to 4
the review must come from either user 123, 265, or 362
CODIGO :
SELECT * FROM reviews WHERE (stars > 2 AND stars <= 4) 
  AND (user_id = 123
  OR user_id = 265
  OR user_id = 362);
### Lección 105
#### Práctica 5 - SQL BETWEEN Practice Exercise
Use the BETWEEN SQL command to find data on medicines:
which sold between 100,000 units and 105,000 units
AND were manufactured by either Biogen, AbbVie, or Eli Lilly
Output the manufacturer name, drug name, and the # of units sold.
CODIGO :
SELECT manufacturer, drug, units_sold 
FROM pharmacy_sales
WHERE (manufacturer = 'Biogen'
  OR manufacturer = 'AbbVie'
  OR manufacturer = 'Eli Lilly')
  AND units_sold BETWEEN 100000 AND 105000;
### Lección 106
#### Práctica 6 - SQL IN Practice Exercise
se the IN SQL command to find data on medicines:
which were manufactured by either Roche, Bayer, or AstraZeneca
and did not sell between 55,000 and 550,000 units
Output the manufacturer name, drug name, and the # of units sold. 
for all the medicines which match that criteria.
CODIGO :
SELECT manufacturer, drug, units_sold FROM pharmacy_sales
WHERE manufacturer IN('Roche','Bayer','AstraZeneca') 
AND units_sold NOT BETWEEN 55000 AND 550000;

### Lección 107
#### Prácticas 7 - SQL LIKE % Practice
You have a table of 1000 customer records from a small-business based in Australia.
Find all customers whose first name starts with "F" and the last letter in their last name is "ck"
CODIGO :
SELECT * FROM customers 
WHERE customer_name LIKE 'F%ck';
#### Práctica 8 - SQL LIKE _ Practice
You have a table of 1000 customer records from a small-business based in Australia.
Find all customers where the 2nd and 3rd letter in their name is "e".
CODIGO :
SELECT *  FROM customers 
WHERE customer_name LIKE '_ee%';

### Lección 108
#### Práctica 9 - SQL Filtering Practice Exercise #1
You have a table of 1000 customer records from a small-business based in Australia.
Find all customers who are between the ages of 18 and 22 (inclusive), live in either Victoria, Tasmania, Queensland,
their gender isn't "n/a", and their name starts with either 'A' or 'B'.
CODIGO :
SELECT *  FROM customers 
WHERE age BETWEEN 18 AND 22
  AND state IN('Victoria','Tasmania','Queensland')
  AND gender !='n/a'
  AND (customer_name LIKE 'A%' OR customer_name LIKE 'B%');

## Intermediate SQL
### Lección 202
#### Práctica 1 - SQL COUNT Practice Exercise
Output the number of rows in the pharmacy_sales table.
CODIGO :
SELECT COUNT(*)  FROM pharmacy_sales;
#### Práctica 2 - SQL SUM Practice Exercise
Imagine you are a Data Analyst working at CVS Pharmacy, and you had access to pharmacy sales data.
Output the total number of drugs manufactured by Pfizer, 
and output the total sales for all the Pfizer drugs.
CODIGO :
SELECT COUNT(manufacturer), SUM(total_sales) 
FROM pharmacy_sales
WHERE manufacturer='Pfizer';
#### Práctica 3 - SQL AVG Practice Exercise
Write a SQL query using AVG to find the average open price for Google stock 
(which has a stock ticker symbol of 'GOOG').
CODIGO :
SELECT AVG(open) 
FROM stock_prices
WHERE ticker='GOOG';
#### Práctica 4 - SQL MIN Practice Exercise: Microsoft Stock
Use SQL's MIN command in this practice exercise, to find the lowest
Microsoft stock (MSFT) ever opened at.
CODIGO :
SELECT MIN(open) 
FROM stock_prices
WHERE ticker='MSFT';
#### Práctica 5 - SQL MAX Practice Exercise: Tesla Stock
Use SQL's MAX command in this practice exercise, to find the highest 
Netflix stock (NFLX) ever opened at.
CODIGO:
SELECT MAX(open) 
FROM stock_prices
WHERE ticker='NFLX';
### Lección 203
#### Práctica 6 - GROUP BY Practice Exercise #1
For every FAANG stock in the stock_prices dataset, write a SQL query to find the lowest price each stock ever opened at?
 Be sure to also order your results by price, in descending order.
CODIGO :
SELECT ticker,MIN(open)
FROM stock_prices
GROUP BY ticker
ORDER BY MIN(open) DESC;
#### Práctica 7 - GROUP BY Practice Exercise #2
This SQL GROUP BY exercise uses real data from a LinkedIn SQL Interview question
which is a bit too hard to tackle right now, so we'll solve an easier variant of the interview question.
Suppose you are given a table of candidates and their skills.
How many candidates possess each of the different skills? Sort your answers based on the count of candidates, from highest to lowest.
CODIGO :
SELECT skill,COUNT(candidate_id) 
FROM candidates
GROUP BY skill
ORDER BY COUNT(candidate_id) DESC;
### Lección 204
#### Práctica 8 - SQL HAVING MIN Practice Exercise
Use SQL's HAVING & MIN commands to find all FAANG stocks whose open share price was always greater than $100.
CODIGO : 
SELECT ticker,MIN(open)
FROM stock_prices
GROUP BY ticker
HAVING MIN(open)>100;
#### Práctica 9 - SQL HAVING Practice Exercise #2
Given a table of candidates and their technical skills, list the candidate IDs of
 candidates who have more than 2 technical skills.
CODIGO :
SELECT candidate_id
FROM candidates
GROUP BY candidate_id
HAVING COUNT(candidate_id)>2;
### Lección 205
#### Práctica 10 - SQL COUNT DISTINCT Practice Exercise
Assume you're given a table containing data on Amazon customers and their spending on products in different category.
 Write a query using COUNT DISTINCT to identify the number of unique products within each product category.
CODIGO :
SELECT category, COUNT(DISTINCT product)
FROM product_spend
GROUP BY category;
### Lección 206
#### Práctica 11 - Practice SQL Subtraction: CVS Pharmacy Interview Question
Write a query to find the top 3 most profitable drugs sold, and how much profit they made.
 Assume that there are no ties in the profits. Display the result from the highest to the lowest total profit.
cogs stands for Cost of Goods Sold which is the direct cost associated with producing the drug.
Total Profit = Total Sales - Cost of Goods Sold
CODIGO :
SELECT drug, total_sales-cogs AS total_profit
FROM pharmacy_sales
GROUP BY drug,total_profit
ORDER BY total_profit DESC
LIMIT 3 ;
#### Práctica 12 - Practice SQL Arithmetic: JPMorgan Chase SQL Interview Question
Your team at JPMorgan Chase is preparing to launch a new credit card, and to gain some insights, 
you're analyzing how many credit cards were issued each month.
Write a query that outputs the name of each credit card and the difference in the number of 
issued cards between the month with the highest issuance cards and the lowest issuance. 
Arrange the results based on the largest disparity.
CODIGO :
SELECT card_name, MAX(issued_amount)-MIN(issued_amount) AS difference
FROM monthly_cards_issued
GROUP BY card_name
ORDER BY difference DESC;

#### Práctica 13 - SQL Math Practice Exercise: Big-Mover Months
What is a big-mover month?
A "big-mover month" is when a stock closes up or down by greater than 10% compared to the price it opened at.
For example, when COVID hit and e-commerce became the new normal, Amazon stock in April 2020 had a big-mover month because 
the price shot up from $96.65 per share at open to $123.70 at close – a 28% increase!
CODIGO :  
SELECT ticker, COUNT(ticker)
FROM stock_prices
WHERE ((close - open)*100)/open > 10 OR ((close - open)*100)/open < -10
GROUP BY ticker
ORDER BY count DESC;
### Lección 207
#### Práctica 14 - SQL CEIL Practice Exercise
Imagine you are a Data Analyst working at CVS Pharmacy, and you had access to pharmacy sales data.
For all Merck drugs, output the drug name, and the unit cost for each drug, rounded up to the nearest dollar. 
Order it from cheapest to most expensive drug.
CODIGO :
SELECT drug, CEIL(total_sales/units_sold) AS unit_cost
FROM pharmacy_sales
WHERE manufacturer = 'Merck'
ORDER BY unit_cost;
### Lección 209
#### Práctica 16 - unfinished Parts
This question is straightforward, so let's approach it with simplicity in both thinking and solution.
Effective April 11th 2023, the problem statement and assumptions were updated to enhance clarity.
CODIGO :
SELECT part, assembly_step
FROM parts_assembly
WHERE finish_date IS NULL;
### Lección 210
#### Práctica 17 - Using CASE-ELSE Clause with CASE Statement in SELECT Statement
Display the actor and character's name, platform, average likes, and the corresponding likes category. 
Sort the results by average likes.
CODIGO :
SELECT actor,character,platform, avg_likes,
CASE 
  WHEN avg_likes >= 15000 THEN 'Super Likes'
  WHEN avg_likes BETWEEN 5000 AND 14999 THEN 'Good Likes'
  ELSE 'Low Likes'
  END AS likes_category
FROM marvel_avengers
ORDER BY avg_likes DESC;
#### Práctica 18 - Laptop vs. Mobile Viewership
Write a query that calculates the total viewership for laptops and mobile 
devices where mobile is defined as the sum of tablet and phone viewership. Output the total 
viewership for laptops as laptop_reviews and the total viewership for mobile devices as mobile_views.
Effective 15 April 2023, the solution has been updated with a more concise and easy-to-understand approach
CODIGO :
SELECT 
  SUM(CASE WHEN device_type = 'laptop' THEN 1 ELSE 0 END) AS laptop_views, 
  SUM(CASE WHEN device_type IN ('tablet', 'phone') THEN 1 ELSE 0 END) AS mobile_views 
FROM viewership;
### Lección 211
#### Práctica 19 - Easy SQL JOIN Practice Exercise
Assume you're given the tables containing info about Robinhood users, and the stock trades they placed.
Use a JOIN to output all the information from the trades table joined to the users table.
CODIGO :
SELECT * 
FROM trades
JOIN users
  ON trades.user_id = users.user_id;
#### Práctica 20 - Harder SQL Join Interview Question
Assume you're given the tables containing completed trade orders and user details in a Robinhood trading system.
Write a query to retrieve the top three cities that have the highest number of completed trade orders listed 
in descending order. Output the city name and the corresponding number of completed trade orders.
CODIGO :
SELECT  city, COUNT(order_id)
FROM trades
JOIN users
  ON trades.user_id = users.user_id
WHERE status = 'Completed'
GROUP BY city
ORDER BY COUNT(order_id) DESC
LIMIT 3 ;
#### Práctica 21 - Handling Nulls + JOIN SQL Interview Question
Assume you're given two tables containing data about Facebook Pages and their respective likes (as in "Like a Facebook Page").
Write a query to return the IDs of the Facebook pages that have zero likes. The output should be sorted in ascending order based on the page IDs.
CODIGO :
SELECT page_id
FROM pages
WHERE NOT EXISTS (
  SELECT page_id
  FROM page_likes AS likes
  WHERE likes.page_id = pages.page_id
;)
### Lección 212
#### Práctica 22 - Extracting Parts from Dates in SQL
Given a table of Facebook posts, for each user who posted at least twice in 2021, write a query to find the number of days between each user’s first post of the year and last post of the year in the year 2021. Output the user and number of the days between each user's first and last post.
p.s. If you've read the Ace the Data Science Interview and liked it, consider writing us a review?
CODIGO :
SELECT 
	user_id, 
    MAX(post_date::DATE) - MIN(post_date::DATE) AS days_between
FROM posts
WHERE DATE_PART('year', post_date::DATE) = 2021 
GROUP BY user_id
HAVING COUNT(post_id)>1;
#### Práctica 23 - Adding and Subtracting Intervals in SQL
Write a query to display the user IDs of those who did not confirm their sign-up on the first day, but confirmed on the second day.
action_date refers to the date when users activated their accounts and confirmed their sign-up through text messages.
CODIGO :
SELECT DISTINCT user_id
FROM emails 
INNER JOIN texts
  ON emails.email_id = texts.email_id
WHERE texts.action_date = emails.signup_date + INTERVAL '1 day'
  AND texts.signup_action = 'Confirmed';
#### Práctica 24 - Facebook/META SQL Interview Question Using Dates
Given a table of Facebook posts, for each user who posted at least twice in 2021, write a query to find the number of days between each user’s first post of the year and last post of the year in the year 2021. Output the user and number of the days between each user's first and last post.
p.s. If you've read the Ace the Data Science Interview and liked it, consider writing us a review?
CODIGO :
SELECT 
	user_id, 
    MAX(post_date::DATE) - MIN(post_date::DATE) AS days_between
FROM posts
WHERE DATE_PART('year', post_date::DATE) = 2021 
GROUP BY user_id
HAVING COUNT(post_id)>1;