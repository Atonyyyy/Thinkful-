Thinkful Airbnb

What's the most expensive listing? What else can you tell me about the listing?
```SQL 
SELECT
sfo_listings.name,
price

FROM
sfo_listings
ORDER BY price DESC
```
Most expensive in  listing in SF is a Victorian house for $10,000. Cheapest listing is $10 for a guest room.
======================

What neighborhoods seem to be the most popular?
```SQL 
SELECT
neighbourhood,
COUNT (*)"sfo_listings.neighbourhood"
FROM
sfo_listings
GROUP BY 1
ORDER BY "sfo_listings.neighbourhood" DESC
```
The Mission, Western Addition, and South of Market are the top 3 most popular SF neighbourhoods.
==============================
What time of year is the cheapest time to go to San Francisco? 
```SQL 
WITH 
	final_table
AS(
WITH 
	clean_table
AS (
SELECT
	EXTRACT (month from calender_date) "date_part",
	REPLACE (REPLACE(REPLACE(price,'$',''),'.00', ''),',','') "clean_price"
FROM 
	sfo_calendar)
SELECT
	date_part,
CAST (clean_price AS int)
FROM
	clean_table)
SELECT
	date_part,
	AVG(clean_price)
FROM
	final_table
GROUP BY date_part
ORDER BY avg ASC
```
=======================
Busiest time?
```SQL
SELECT
EXTRACT(MONTH FROM sfo_calendar.calender_date) "date_part",
Count (*) as available 
FROM
sfo_calendar
WHERE
available = 'f'
GROUP BY date_part
ORDER BY available DESC
```
The busiest month would be based on how many airbnbs’ are not available in San Francisco (meaning they are probably booked). With that said, August looks to be the busiest month with 145,379 listings booked. The next 2 busiest months would be October with 125,929 listings booked and July with 121,473 listings booked. 



