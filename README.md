--  # SQL-for-Data-Science-Certification
--  The Final Project for UC Davis Certification on Coursera
--  Part 1: Yelp Dataset Profiling and Understanding

--  1.  Profile the data by finding the total number of records for each of the tables below:
--Table Name 
COUNT(*)
business
10000
hours
10000
category
10000
attribute
10000
review
10000
checkin
10000
photo
10000
user
10000
friend
10000
elite_years
10000
tip
10000

--2.  Find the total distinct records by either the foreign key or primary key for each table. 
    If two foreign keys are listed in the table, please specify which foreign key.
Table Name COUNT(DISTINCT ...)
business
Id 10000
hours
business_id 1562
category
business_id 2643
attribute
business_id 1115
review
business_id 8090 user_id 9581
checkin
business_id 493
photo
id 10000 business_id 6493
user
name 3454
friend
user_id 11
elite_years
user_id 2780
tip
business_id 3979 user_id 537

--Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.

--3.  Are there any columns with null values in the Users table? Indicate "yes," or "no." Answer:
--A.  No
--SQL code used to arrive at answer:
SELECT 
  id,
  name, 
  review_count, 
  yelping_since, 
  useful,
  funny,
  cool,
  fans, 
  average_stars,
  compliment_hot, 
  compliment_more, 
  compliment_profile, 
  compliment_cute,
  compliment_list, 
  compliment_note, 
  compliment_plain, 
  compliment_cool, 
  compliment_funny, 
  compliment_writer, 
  compliment_photos
FROM
  user
WHERE
     id                   IS NULL
  OR name                 IS NULL
  OR review_count         IS NULL
  OR yelping_since        IS NULL
  OR useful               IS NULL
  OR funny                IS NULL
  OR cool                 IS NULL
  OR fans                 IS NULL
  OR average_stars        IS NULL
  OR compliment_hot       IS NULL
  OR compliment_more      IS NULL 
  OR compliment_profile   IS NULL 
  OR compliment_cute      IS NULL 
  OR compliment_list      IS NULL 
  OR compliment_note      IS NULL 
  OR compliment_plain     IS NULL 
  OR compliment_cool      IS NULL 
  OR compliment_funny     IS NULL 
  OR compliment_writer    IS NULL 
  OR compliment_photos    IS NULL
  
--4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:
--i. Table: Review, Column: Stars
--min: 1 max: 5 avg: 3.7082
--ii. Table: Business, Column: Stars
--min: 1.0 max: 5.0 avg: 3.6549
--iii. Table: Tip, Column: Likes
--min: 0 max: 2 avg: 0.0144
--iv. Table: Checkin, Column: Count
--min: 1 max: 53 avg: 1.9414
--v. Table: User, Column: Review_count
--min: 0 max: 2000 avg: 24.2995

--5. List the cities with the most reviews in descending order: 

--SQL code used to arrive at answer:
SELECT 
  city,
  SUM(review_count)
FROM
  business
GROUP BY 
  city
ORDER BY
   SUM(review_count) DESC;
   

+-----------------+-------------------+ 
| city            | sum(review_count) | 
+-----------------+-------------------+
| Las Vegas       |             82854 |
| Phoenix         |             34503 |
| Toronto         |             24113 |
| Scottsdale      |             20614 |
| Charlotte       |             12523 |
| Henderson       |             10871 |
| Tempe           |             10504 |
| Pittsburgh      |              9798 |
| Montreal        |              9448 |
| Chandler        |              8112 |
| Mesa            |              6875 |
| Gilbert         |              6380 |
| Cleveland       |              5593 |
| Madison         |              5265 |
| Glendale        |              4406 |
| Mississauga     |              3814 |
| Edinburgh       |              2792 |
| Peoria          |              2624 |
| North Las Vegas |              2438 |
| Markham         |              2352 |
| Champaign       |              2029 |
| Stuttgart       |              1849 |
| Surprise        |              1520 |
| Lakewood        |              1465 |
| Goodyear        |              1155 |
+—————————————————|——————————————————-+
(Output limit exceeded, 25 of 362 total rows shown)

--6. Find the distribution of star ratings to the business in the following cities:
--i. Avon
--SQL code used to arrive at answer:
SELECT
  stars,
  sum(review_count)
AS
  starcount
FROM
  business
WHERE
  city = 'Avon'
GROUP BY
   stars;
--Copy and Paste the Resulting Table Below (2 columns – star rating and count):
+-------+-----------+
| stars | starcount | 
+-------+-----------+ 
| 1.5   |         10| 
| 2.5   |          6| 
| 3.5   |         88| 
| 4.0   |         21| 
| 4.5   |         31| 
| 5.0   |          3| 
+———————+————————-——+
