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

--ii. Beachwood
--SQL code used to arrive at answer:
SELECT
      stars,
      sum(review_count)
AS
starcount
FROM
      business
WHERE
      city = 'Beachwood'
GROUP BY
      stars;
--Copy and Paste the Resulting Table Below (2 columns – star rating and count):
+-------+----------+
|2.0    |         8|   
|2.5.   |         3|
|3.0    |        11|
|3.5    |         6|
|4.0    |        69|
|4.5    |        17|
|5.0    |        23|
+-------+----------+
       
--7. Find the top 3 users based on their total number of reviews: 
--SQL code used to arrive at answer:
SELECT name,
    review_count
FROM
user
ORDER BY
      review_count DESC;
--Copy and Paste the Result Below:
+-----------+--------------+ 
| name      | review_count | 
+-----------+--------------+
| Gerald    |         2000 |
| Sara      |         1629 |
| Yuri      |         1339 |
| .Hon      |         1246 |
| William   |         1215 |
| Harald    |         1153 |
| eric      |         1116 |
| Roanna    |         1039 |
| Mimi      |          968 |
| Christine |          930 |
| Ed        |          904 |
| Nicole    |          864 |
| Fran      |          862 |
| Mark      |          861 |
| Christina |          842 |
| Dominic   |          836 |
| Lissa     |          834 |
| Lisa      |          813 |
| Alison    |          775 |
| Sui       |          754 |
| Tim       |          702 |
| L         |          696 |
| Angela    |          694 |
| Crissy    |          676 |
| Lyn       |          675 |
+-----------+--------------+

--8. Does posing more reviews correlate with more fans?
--No.
--Please explain your findings and interpretation of the results:
--I searched for the number of reviews, fans and usefulness of the reviews by joining tables “user” and “review” 
--and sorted the data in descending order according to 1, number of reviews; 2, fans; and 3, useful. There is no correlation between the
--number of fans and the number of reviews seen in this query nor how useful they are to fans.
--User “LeeAnn” had 10 useful reviews out of 11 with a ratio of 91% correlation. User “LeeAnn” has zero fans. 
--Therefore, the usefulness of the review does not reflect gaining fans.
--However, user “Cynthia” has an almost equal number of reviews and fans ratio, 83%, with only one review being useful. 
--Of the 73 rows of data, following her interactions could determine how a user gets more “fans.”

--9. Are there more reviews with the word "love" or with the word "hate" in them? 
--Answer:
--Love
+------+-------------+ 
| Word | Total Count | 
+------+-------------+ 
| hate |         232 | 
| love |        1780 |
+------+-------------+
--SQL code used to arrive at answer:
SELECT
      'love' Word, COUNT(text) [Total Count]
FROM
review
WHERE
      text LIKE '%love%'
UNION SELECT
      'hate' Word, COUNT(text) [Total Count]
FROM
review
WHERE
text LIKE ‘%hate%';

--Part 2: Inferences and Analysis

--1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. 
--Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.

--i. Do the two groups you chose to analyze have a different distribution of hours?
--Yes. Some businesses are open half a day and others are open for more than 12 hours.

--ii. Do the two groups you chose to analyze have a different number of reviews?
--Yes, and it looks like the more of an impression or experience is made on the reviewer, the more likely they will publish a review- 
--either positive or negative.

--iii. Are you able to infer anything from the location data provided between these two groups? Explain.
--From this specific query, not much can be inferred as only two days of hours appeared. It can be inferred that the more reviews a business has, 
--the more their score meets the median score of 3.0 stars as the reviews can increase or decrease the rating.

SQL code used for analysis:
SELECT 
    business.name,
    business.city, 
    business.stars, 
    hours.hours,
    business.review_count
FROM
    business
INNER JOIN
    category 
ON
    business.id = category.business_id
INNER JOIN 
    hours
ON
    hours.business_id = business.id
WHERE
    business.city = 'Phoenix'
GROUP BY 
    business.name;
    
--2. Group business based on the ones that are open and the ones that are closed. What differences can you find between 
--the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.

--i. Difference 1:
--The Average Review Count for ‘open’ businesses is higher than those that are closed.

--ii. Difference 2:
--The Average Stars for ‘open’ businesses is slightly higher than those businesses that are closed even though there are 
--more reviews for ‘open’ businesses.
--SQL code used for analysis:
SELECT  
    AVG(review_count),
    AVG(stars),
    is_open
FROM
      business
GROUP BY
      is_open;
      
--3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the 
--Yelp dataset and are going to prepare the data for analysis.
--Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses
--to find commonalities or anomalies between them, predicting the overall star rating for a business, 
--predicting the number of fans a user will have, and so on. These are just a few examples to get you started, 
--so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:

--i. Indicate the type of analysis you chose to do:
--To determine if the number of fans correlates to the number of useful reviews written by users.

--ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
--To determine is a user acquires fans through useful reviews, comparisons between the top 25 user names with 
--the highest number of review_count, fans, and useful reviews. 
--This will help to narrow dow the top users with the highest of all 3 consecutively.

--iii. Provide the SQL code you used to create your final dataset:
SELECT 
    name,
    review_count,
    fans,
    useful
FROM
    user
ORDER BY
     /*enter row*/ DESC
LIMIT 15;
