# Exercise Part 1: SQLZoo
- [X] head to SQL Zoo and complete tutorials 0, 1, 2, and 3.

# Exercise Part 2: More SQL
- [X] WHERE and ORDER BY
- [X] Simple SUM
- [X] Simple MIN/MAX
- [X] Find all active students
- [X] Simple GROUP BY
- [X] Simple Having
- [X] Complete Tutorial 5 (SUM_AND_COUNT)

# Exercise Part 3: Products Querying

1. Add a product to the table with the name of “chair”, price of 44.00, and can_be_returned of false.
```sql
INSERT INTO products (name, price, can_be_returned)
    VALUES ('chair', 44.00, false);
```

2. Add a product to the table with the name of “stool”, price of 25.99, and can_be_returned of true.
```sql
INSERT INTO products (name, price, can_be_returned)
    VALUES ('stool', 25.99, true);
```

3. Add a product to the table with the name of "table", price of 124.00, and can_be_returned of false.
```sql
INSERT INTO products (name, price, can_be_returned)
    VALUES ('table', 124.00, false);
```
4. Display all of the rows and columns in the table.
```sql
SELECT * FROM products;
```

5. Display all of the names of the products.
```sql
SELECT name FROM products;
```

6. Display all of the names and prices of the products.
```sql
SELECT name, price FROM products
```

7. Add a new product - make up whatever you would like!
```sql
INSERT INTO products (name, price, can_be_returned)
    VALUES ('$25 Bill', 30.00, false);
```

8. Display only the products that **can_be_returned**.
```sql
SELECT * 
    FROM products 
    WHERE can_be_returned = false;
```

9. Display only the products that have a price less than 44.00.
```sql
SELECT *
    FROM products
    WHERE price < 44.00;
```

10. Display only the products that have a price in between 22.50 and 99.99.
```sql
SELECT *
    FROM products
    WHERE price > 22.50 AND price < 99.99;
```

11. There's a sale going on: Everything is $20 off! Update the database accordingly.
```sql
UPDATE products SET price = price-20;
```

12. Because of the sale, everything that costs less than $25 has sold out. Remove all products whose price meets this criteria.
```sql
DELETE FROM products WHERE price < 25;
```

13. And now the sale is over. For the remaining products, increase their price by $20.
```sql
UPDATE products SET price = price+20;
```

14. There is a new company policy: everything is returnable. Update the database accordingly.
```sql
UPDATE products SET can_be_returned = true;
```
# Exercise Part 4: Google Play Store Querying
1. Find the app with an ID of ***1880***
```sql
SELECT * 
    FROM analytics 
    WHERE id = 1880;
```
`Output`
```
-[ RECORD 1 ]---+------------------------
id              | 1880
app_name        | Web Browser for Android
category        | PRODUCTIVITY
rating          | 4.3
reviews         | 144879
size            | Varies with device
min_installs    | 10000000
price           | 0
content_rating  | Everyone
genres          | {Productivity}
last_updated    | 2016-01-24
current_version | 3.5.0
android_version | Varies with device
```

2. Find the ID and app name for all apps that were last updated on August 01, 2018
```sql
SELECT id, app_name
    FROM analytics
    WHERE last_updated = '2018-8-01'
```
`output`
```
  id  |                                     app_name                                      
------+-----------------------------------------------------------------------------------
   10 | Clash Royale
   11 | Candy Crush Saga
   12 | UC Browser - Fast Download Private & Secure
   74 | Score! Hero
  101 | Tiny Flashlight + LED
  102 | Crossy Road
  103 | SimCity BuildIt
  111 | FIFA Soccer
  112 | Angry Birds 2
  125 | Need for Speed™ No Limits

-- NOTE: Cut off to just 10 queries

```

3. Count the number of apps in each category, e.g. “Family | 1972”.
```sql
SELECT distinct(category), COUNT(category) FROM analytics GROUP BY category;
```
`output`
```
      category       | count 
---------------------+-------
 ART_AND_DESIGN      |    63
 AUTO_AND_VEHICLES   |    75
 BEAUTY              |    46
 BOOKS_AND_REFERENCE |   191
 BUSINESS            |   313
 COMICS              |    59
 COMMUNICATION       |   342
 DATING              |   204
 EDUCATION           |   156
 ENTERTAINMENT       |   149
 EVENTS              |    52
 FAMILY              |  1789
 FINANCE             |   331
 FOOD_AND_DRINK      |   110
 GAME                |  1110
 HEALTH_AND_FITNESS  |   298
 HOUSE_AND_HOME      |    82
 LIBRARIES_AND_DEMO  |    80
 LIFESTYLE           |   319
 MAPS_AND_NAVIGATION |   129
 MEDICAL             |   350
 NEWS_AND_MAGAZINES  |   249
 PARENTING           |    59
 PERSONALIZATION     |   329
 PHOTOGRAPHY         |   313
 PRODUCTIVITY        |   360
 SHOPPING            |   241
 SOCIAL              |   269
 SPORTS              |   338
 TOOLS               |   753
 TRAVEL_AND_LOCAL    |   234
 VIDEO_PLAYERS       |   165
 WEATHER             |    79
```

5. Find the top 5 most-reviewed apps and the number of reviews for each.
```sql
SELECT id, app_name, reviews 
FROM analytics 
ORDER BY reviews DESC
FETCH NEXT 5 ROWS ONLY;
```
`output`
```
 id |                 app_name                 | reviews  
----+------------------------------------------+----------
  1 | Facebook                                 | 78158306
  2 | WhatsApp Messenger                       | 78128208
  3 | Instagram                                | 69119316
  4 | Messenger – Text and Video Chat for Free | 69119316
  5 | Clash of Clans                           | 69109672
```

6. Find the average rating for each category ordered by the highest rated to lowest rated.
```sql
SELECT DISTINCT(category), AVG(rating) FROM analytics GROUP BY category ORDER BY AVG(rating) desc;
```
`output`
```
      category       |        avg         
---------------------+--------------------
 EVENTS              |  4.395238104320708
 EDUCATION           |   4.38903223006956
 ART_AND_DESIGN      |  4.347540949211746
 BOOKS_AND_REFERENCE | 4.3423728633061645
 PERSONALIZATION     |    4.3283387457509
 BEAUTY              |  4.299999970656175
 GAME                |  4.287167731498383
 PARENTING           |  4.285714266251545
 HEALTH_AND_FITNESS  | 4.2743944663902464
 SHOPPING            |  4.253648051376507
 SOCIAL              |  4.245669291244717
 WEATHER             |   4.24399998664856
 SPORTS              |  4.233333332576449
 PRODUCTIVITY        |  4.212173904543338
 AUTO_AND_VEHICLES   |  4.200000017881393
 HOUSE_AND_HOME      |  4.197368430463891
 PHOTOGRAPHY         |  4.196116511489967
 MEDICAL             | 4.1926829182520144
 FAMILY              | 4.1904873752761995
 LIBRARIES_AND_DEMO  | 4.1784615259904125
 FOOD_AND_DRINK      |  4.155660354866172
 COMICS              |  4.155172401461108
 COMMUNICATION       |  4.151234589241169
 FINANCE             |  4.146835436549368
 NEWS_AND_MAGAZINES  |  4.130131007281974
 ENTERTAINMENT       |   4.12617449632427
 BUSINESS            |  4.116666667004849
 TRAVEL_AND_LOCAL    |   4.10179372753263
 LIFESTYLE           |  4.077076400237226
 VIDEO_PLAYERS       |  4.059748438919115
 MAPS_AND_NAVIGATION |  4.058196711735647
 TOOLS               |  4.050627608678331
 DATING              |  3.993684190825412
 ```

7. Find the name, price, and rating of the most expensive app with a rating that's less than 3
```sql
SELECT name, price, rating
    FROM analytics
    ORDER BY price DESC
    WHERE rating < 3;
    LIMIT 1;
```
`output`
```
      app_name      | price  | rating 
--------------------+--------+--------
 Naruto & Boruto FR | 379.99 |    2.9
```

8. Find all apps with a min install not exceeding 50, that have a rating. Order your results by highest rated first.
```sql
SELECT app_name, rating, min_install
    FROM analytics
    WHERE min_install < 50 AND rating IS NOT NULL;
    ORDER BY rating desc;
```

9. Find the names of all apps that are rated less than 3 with at least 10000 reviews
```sql
SELECT app_name
    FROM analytics
    WHERE rating < 3 AND reviews > 10000;
```

10. Find the top 10 most-reviewed apps that cost between 10 cents and a dollar.
```sql
SELECT id, app_name, reviews, price
FROM analytics
WHERE price > 0.10 AND price < 1.00
ORDER BY reviews desc
LIMIT 10;
```

11. Find the most out of date app. *Hint: you don't need to do it this way, but it's possible to do with a subquery*

```sql
SELECT app_name, last_updated FROM analytics ORDER BY last_updated LIMIT 1;
```
`output`
```
  app_name  | last_updated 
------------+--------------
 CP Clicker | 2010-05-21
```

12. Find the most expensive app (the query is very similar to #11)
```sql
SELECT app_name, price FROM analytics ORDER BY price desc LIMIT 1;
```
`output`
```
      app_name      | price 
--------------------+-------
 Cardi B Piano Game |   400
```
13. Count all the reviews in the Google Play Store.
```sql
SELECT SUM(reviews) FROM analytics;
```
`output`
```
    sum     
------------
 4814575866
```

14. Find all the categories that have more than 300 apps in them.
```sql
SELECT DISTINCT(category), COUNT(category) FROM analytics GROUP BY category HAVING COUNT(category) > 300 ORDER BY COUNT(category) desc;
```
`output`
```
    category     | count 
-----------------+-------
 FAMILY          |  1789
 GAME            |  1110
 TOOLS           |   753
 PRODUCTIVITY    |   360
 MEDICAL         |   350
 COMMUNICATION   |   342
 SPORTS          |   338
 FINANCE         |   331
 PERSONALIZATION |   329
 LIFESTYLE       |   319
 BUSINESS        |   313
 PHOTOGRAPHY     |   313
```

15. Find the app that has the highest proportion of min_installs to review, among apps that have been installed at least 100,000 times. Display the name of the app along with the number of reviews, the min_installs, and the proportion.

```sql
SELECT app_name, min_installs, reviews, min_installs/reviews AS installs_over_reviews
FROM analytics
WHERE min_installs > 100000 
ORDER BY min_installs/reviews DESC;
```
