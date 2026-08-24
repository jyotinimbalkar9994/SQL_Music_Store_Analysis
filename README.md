README.md
SQL Music Store Analysis
📌 Project Overview

This project contains a collection of SQL queries designed to analyze data from a music store database. The project uses the Chinook-style relational database and demonstrates SQL concepts ranging from basic filtering and aggregation to advanced CTEs, joins, subqueries, and window functions.

The questions are divided into three difficulty levels:

Easy – Basic sorting, grouping, aggregation, and joins
Moderate – Multiple-table joins, subqueries, and filtering
Advanced – CTEs, window functions, ranking, and complex joins

The goal of this project is to strengthen practical SQL skills and answer real-world business questions using relational data.

🗂️ Database Schema

The project works with tables such as:

customer – Customer information
invoice – Customer invoices and billing information
invoice_line – Individual products/tracks purchased in each invoice
track – Music track information
album – Album information
artist – Artist information
genre – Music genre information
employee – Employee information
Main Relationships
Employee

Customer
   │
   └── Invoice
          │
          └── InvoiceLine
                 │
                 └── Track
                       │
                       ├── Album
                       │      └── Artist
                       │
                       └── Genre

📊 Question Sets
Question Set 1 – Easy
Q1. Senior Most Employee

Find the employee with the highest job level.

Concepts:

ORDER BY
DESC
LIMIT
Q2. Countries With the Most Invoices

Determine which countries have generated the highest number of invoices.

Concepts:

COUNT()
GROUP BY
ORDER BY
Q3. Top 3 Invoice Values

Return the three largest invoice totals.

Concepts:

Sorting
DESC
LIMIT
Q4. City With the Best Customers

Find the city that has generated the highest total invoice revenue.

Concepts:

SUM()
GROUP BY
Sorting aggregated results
LIMIT
Q5. Best Customer

Identify the customer who has spent the most money.

Concepts:

JOIN
SUM()
GROUP BY
Aggregation
Sorting
📈 Question Set 2 – Moderate
Q1. Rock Music Listeners

Find all customers who have purchased Rock music.

Return:

Email
First name
Last name
Genre

Sort the results alphabetically by email.

Concepts:

Multiple JOINs
DISTINCT
Filtering
Subqueries
Q2. Top 10 Rock Artists

Find the top 10 artists who have written the most Rock tracks.

Return:

Artist ID
Artist name
Number of Rock tracks

Concepts:

Multiple-table joins
COUNT()
GROUP BY
Filtering by genre
Ranking using ORDER BY
Q3. Tracks Longer Than Average

Find all tracks whose length is greater than the average track length.

Return:

Track name
Track length in milliseconds

Sort from longest to shortest.

Concepts:

AVG()
Subqueries
Comparison with aggregate results
Sorting
🚀 Question Set 3 – Advanced
Q1. Customer Spending on the Best-Selling Artist

First identify the artist who generated the highest revenue.

Then determine how much each customer spent on that artist.

Return:

Customer ID
First name
Last name
Artist name
Amount spent

Concepts:

CTEs
Multiple-table joins
SUM()
GROUP BY
Revenue calculation using:
unit_price * quantity


This query demonstrates why invoice_line should be used when calculating revenue for individual products or artists instead of relying only on the invoice total.

Q2. Most Popular Genre by Country

Determine the most popular music genre in each country based on the number of purchased tracks.

If multiple genres have the same highest number of purchases, return all tied genres.

Concepts:

CTEs
Aggregation
COUNT()
Country-level grouping
Ranking
Handling ties

A ranking function such as RANK() is preferable when ties must be preserved.

Q3. Highest-Spending Customer by Country

Find the customer who has spent the most money in each country.

If multiple customers share the highest spending amount, return all tied customers.

Return:

Country
Customer ID
First name
Last name
Total spending

Concepts:

CTEs
SUM()
MAX()
GROUP BY
Joins between aggregated datasets
Handling ties
🧠 SQL Concepts Demonstrated

This project covers several important SQL concepts:

Basic SQL
SELECT
WHERE
ORDER BY
LIMIT
DISTINCT
Aggregate Functions
COUNT()
SUM()
AVG()
MAX()
Grouping
GROUP BY
Aggregation by customer
Aggregation by country
Aggregation by artist
Aggregation by genre
Joins
INNER JOIN
Joining multiple related tables
Understanding relational database relationships
Subqueries

Used for questions such as:

WHERE milliseconds > (
    SELECT AVG(milliseconds)
    FROM track
)

Common Table Expressions

CTEs make complex queries easier to read and organize:

WITH best_selling_artist AS (
    ...
)
SELECT ...

Window Functions

Window functions are useful for ranking records within groups:

ROW_NUMBER() OVER (
    PARTITION BY country
    ORDER BY total_spending DESC
)


For problems where ties must be retained:

RANK() OVER (
    PARTITION BY country
    ORDER BY total_spending DESC
)

🔍 Key SQL Learning Points
1. ROW_NUMBER() vs RANK()

ROW_NUMBER() assigns a unique position to every row.

For example:

Customer A   1000   1
Customer B   1000   2
Customer C    800   3


When the requirement is to return all customers tied for first place, RANK() is more appropriate:

Customer A   1000   1
Customer B   1000   1
Customer C    800   3


Therefore, tie-based questions should generally use RANK() rather than ROW_NUMBER().

2. Invoice vs Invoice Line

The invoice table contains the total for an invoice, while invoice_line contains individual purchased tracks.

For artist-level or track-level revenue calculations, use:

SUM(unit_price * quantity)


This allows revenue to be correctly attributed to the specific tracks and artists purchased.

3. Aggregation Before Ranking

Many advanced questions follow this pattern:

Raw transaction data
        ↓
GROUP BY
        ↓
Calculate totals/counts
        ↓
Rank or find MAX
        ↓
Return top result(s)


Understanding this pattern is essential for solving analytical SQL problems.

🛠️ Tools & Technologies
SQL
Relational Database
PostgreSQL Music Store Dataset
SQL-compatible database such as PostgreSQL
📁 Suggested Project Structure
sql-music-store-analysis/
│
├── README.md
│
├── sql/
│   ├── easy.sql
│   ├── moderate.sql
│   └── advanced.sql
│
└── dataset/
    └── PostgreSQL_database

🎯 Project Objectives

The main objectives of this project are to:

Practice SQL fundamentals.
Understand relationships between relational tables.
Perform customer and sales analysis.
Work with multiple-table joins.
Use aggregate functions for business analysis.
Understand subqueries and CTEs.
Apply window functions for ranking.
Handle ties correctly in analytical queries.
Solve real-world business questions using SQL.
📌 Example Business Questions

The analysis can answer questions such as:

Who is the company's senior-most employee?
Which countries generate the most invoices?
Which city generates the most revenue?
Who is the highest-spending customer?
Which artists have the most Rock tracks?
Which tracks are longer than average?
Which artist generates the most revenue?
What genre is most popular in each country?
Who is the highest-spending customer in each country?
📚 What I Learned

Through this project, I practiced transforming raw relational data into meaningful business insights using SQL.

The project particularly focuses on moving from simple queries to more advanced analytical techniques such as CTEs, multi-table joins, aggregation, subqueries, window functions, ranking, and tie handling.

⭐ Conclusion

This project demonstrates a progression from basic SQL queries to advanced data analysis techniques using a music-store database.

It serves as a practical SQL portfolio project and can be used to demonstrate knowledge of relational databases, data analysis, and business-oriented SQL problem solving.
