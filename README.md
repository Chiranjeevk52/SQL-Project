


# Music Store Analysis


## OBJECTIVE

This project has been  made using SQL. It helps the owner of  Digital Music Store understand their customers better. 
## Problem Set

1. Who is the senior most employee based on job title?
2. Which countries have the most Invoices?
3. What are top 3 values of total invoice?
4. Which city has the best customers? We would like to throw a promotional Music Festival in the city we made the most money. Write a query that returns one city that has the highest sum of invoice totals. Return both the city name & sum of all invoice totals.

5. Who is the best customer? The customer who has spent the most money will be declared the best customer. Write a query that returns the person who has spent the most money.

6. Write query to return the email, first name, last name, & Genre of all Rock Music listeners. Return your list ordered alphabetically by email starting with A
7. Return all the track names that have a song length longer than the average song length. Return the Name and Milliseconds for each track. Order by the song length with the longest songs listed first.


### PROJECT KEY POINTS
1. Data collection
2. Data cleaning & wrangling
3. Uploading csv file to SQL server
4. Writing qeuries according to question

## Queries
1.  SELECT title, last_name, first_name 
    FROM employee

    ORDER BY levels DESC

2.  SELECT COUNT(*) AS c, billing_country 
    FROM invoice

    GROUP BY billing_country

    ORDER BY c DESC

3.  SELECT total 
    FROM invoice

    ORDER BY total DESC

4. SELECT billing_city,SUM(total) AS InvoiceTotal
    FROM invoice

    GROUP BY billing_city

    ORDER BY InvoiceTotal DESC

5. SELECT DISTINCT email,first_name, last_name
    FROM customer

    JOIN invoice ON customer.customer_id = invoice     customer_id

    JOIN invoice_line ON invoice.invoice_id = invoice_line.invoice_id

    WHERE track_id IN(

	SELECT track_id FROM track

	JOIN genre ON track.genre_id = genre.genre_id

	WHERE genre.name LIKE 'Rock'
)
    ORDER BY email;

6. SELECT DISTINCT email AS Email,first_name AS        FirstName, last_name AS LastName, genre.name AS Name
FROM customer

    JOIN invoice ON invoice.customer_id = customer.customer_id

    JOIN invoice_line ON invoice_line.invoice_id = invoice.invoice_id

    JOIN track ON track.track_id = invoice_line.track_id

    JOIN genre ON genre.genre_id = track.genre_id

    WHERE genre.name LIKE 'Rock'

    ORDER BY email;

7. SELECT name,milliseconds
    FROM track

    WHERE milliseconds > (

	SELECT AVG(milliseconds) AS avg_track_length
	FROM track )

    ORDER BY milliseconds DESC;





