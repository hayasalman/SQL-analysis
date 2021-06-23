# SQL-analysis
sql queries
SELECT g.name AS Music_type, COUNT(*) AS rank
FROM Customer c
JOIN invoice i ON i.customerid = c.customerid 
JOIN invoiceline line ON line.invoiceid = i.InvoiceId
JOIN track t ON t.trackid = line.trackid 
JOIN genre g ON g.genreid = t.genreid 
WHERE c.country  = 'Germany'
GROUP BY 1
ORDER BY 2 DESC ;
\\

Query 2 \\

WITH table1 AS (SELECT al.Title album_title, AVG(t.milliseconds), CASE WHEN t.Milliseconds > AVG(t.milliseconds) THEN 'Above'
ELSE 'Below' END AS period 
FROM track t
JOIN album al ON al.albumid = t.AlbumId 
GROUP BY 1
ORDER BY 1)
SELECT period,COUNT(*) 
FROM table1
WHERE period IN ('Below' , 'Above' ) 
GROUP BY 1;
\\


QUERY 3 \\
 
SELECT c.firstname || ' ' || c.lastname AS customer_name , c.email ,c.country , SUM (i.total) AS total_amount
FROM customer c
JOIN invoice i ON c.customerid = i.customerid 
GROUP BY 1
ORDER BY 4 DESC 
LIMIT 10 ;

\\


QUERY 4 \\

SELECT DISTINCT a.name singer, COUNT(*) songs
FROM artist a
JOIN album al ON al.artistid = a.artistid 
JOIN track t ON t.albumid = al.albumid 
JOIN genre g ON g.genreid = t.genreid 
WHERE g.name = 'Jazz'
GROUP BY 1 
ORDER by 2 DESC 
LIMIT 5;
