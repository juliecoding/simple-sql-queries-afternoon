# simple-sql-queries

For today we will be practicing inserting and querying data using SQL.

Here is a website that will let us write queries to interact with some data.  [http://jxs.me/chinook-web/](http://jxs.me/chinook-web/)

On the left are the Tables with their fields.  The right is where we will be writing our queries.  The bottom is where we will see our results.  

Any new tables or records that we add into the database will be removed after you refresh the page.  So if you're wondering where you data went, that may be why.

Use [www.sqlteaching.com](http://www.sqlteaching.com/) or [sqlbolt.com](http://sqlbolt.com/) as resources for the missing keywords you'll need.

## PERSON
1. Create a table called Person that records a person's Name, Age, Height, City, FavoriteColor, and Id.  Id should be an auto-incrementing id/primary key.  

  CREATE TABLE Person
  (
  Name VARCHAR(255),
  Age INTEGER,
  Height VARCHAR(255),
  City VARCHAR(255),
  FavoriteColor VARCHAR(255),
  Id INTEGER PRIMARY KEY AUTOINCREMENT
  )

2. Add 5 different people into the Person database.  Remember to not include the Id because it should auto-increment.
  INSERT INTO Person (Name, Age, Height, City, FavoriteColor)
  VALUES ("bob", 25, 180, "Brooklyn", "purple"),
  ("sam", 30, 185, "Boston", "red"),
  ("frida", 35, 190, "El Paso", "indigo"),
  ("wheland", 40, 195, "Detroit", "green"),
  ("gyorgy", 45, 200, "Albuquerque", "gold")

3. List the people in the Person table by Height from tallest to shortest (descending)
  SELECT * FROM Person ORDER BY height desc

(For this database to create an auto incrementing field set it's type to INTEGER PRIMARY KEY AUTOINCREMENT)

  * List the people in the Person table by Height from shortest to tallest (ascending)
      SELECT * FROM Person ORDER BY height

  * List all the people in the Person table by oldest first
      SELECT * FROM Person ORDER BY age DESC

  * List all the people in the Person table older than age 20.
      SELECT * FROM Person WHERE age > 20

  * List all the people in the Person table that are exactly 18.
      SELECT * FROM Person WHERE age = 18;

  * List all Person that are less than 20 and older than 30.
      SELECT * FROM Person WHERE age < 20 OR age > 30;

  * List all Person that are not 27 (Use not equals)
      SELECT * FROM Person WHERE age != 27;

  * List all Person where their favorite color is not red
      SELECT * FROM Person WHERE favoriteColor != "red";

  * List all Person where their favorite color is not red or blue
      SELECT * FROM Person WHERE favoriteColor != "red" OR favoriteColor != "blue";

  * List all Person where their favorite color is orange or green
      SELECT * FROM Person WHERE favoriteColor = "orange" OR favoriteColor = "green";

  * List all Person where their favorite color is orange, green or blue (use IN)
      SELECT * FROM Person WHERE favoriteColor IN ("orange", "green", "blue")

  * List all Person where their favorite color is yellow or purple
      SELECT * FROM Person WHERE favoriteColor IN ("yellow", "purple")

## ORDER
4. Create a table called Orders that records the productName, productPrice, Quantity, and personId  
    CREATE TABLE Orders
      (
        productName varchar (255),
        productPrice FLOAT,
        quantity INTEGER,
        personId INTEGER
      )


5. Add 5 Orders to Order table
    INSERT INTO Orders (productName, productPrice, quantity, personId)
    VALUES ("robot vacuum", $200, 5, 1),
    ("whiteboard", $10, 10, 12),
    ("wheely chair", $50, 2, 123),
    ("book", $15, 8, 1234),
    ("smartphone", $500, 1, 12345)

6. Select all the records from the Order table
    SELECT * FROM Orders

  * Calculate the total number of products Ordered
      SELECT sum(quantity) as Total_orders FROM Orders

  * Calculate the total Order Price
      <!-- SELECT sum(productPrice) FROM Orders 2CB2 -->

  * Calculate the total Order Price By personId (If you only made orders for 1 person, go add more for the other people)
      SELECT personId, sum(productPrice) FROM Orders GROUP BY personId

## Artists
7. Add 3 new Artists to the Artist table
      INSERT INTO Artist (Name)
      VALUES ("Paul McCartney"), ("Gluck"), ("Regina Spektor")

 * Select the top 10 artists in reverse alphabetical order
      SELECT * FROM Artist ORDER BY ArtistId desc LIMIT 10

 * Select the top 5 artists in alphabetical order
      SELECT * FROM Artist ORDER BY Name LIMIT 5

 * Select all artists that start with the word Black
      SELECT * FROM Artist WHERE Name LIKE "Black%"

 * Select all artists that contain the word Black
      SELECT * FROM Artist WHERE Name LIKE "%Black%"

## Employee
8. Add 2 new Employees to the Employee table
      INSERT INTO EMPLOYEE (lastName, firstName)
      VALUES ("Darin", "Bobby"), ("Jangles", "Bo")

* List all Employee first and last names only that live in Calgary
      SELECT lastName, firstName FROM Employee WHERE City like "calgary"

* Find the first and last name for the youngest employee
      SELECT lastName, firstName FROM Employee ORDER BY Birthdate DESC LIMIT 1

* Find the first and last name for the oldest employee
      SELECT lastName, firstName FROM Employee ORDER BY Birthdate LIMIT 1

* Find everyone that reports to Nancy Edwards (Use the ReportsTo column)
      SELECT lastName, firstName, reportsto FROM Employee ORDER BY reportsto

* Count how many people live in Lethbridge
      SELECT COUNT(*) FROM Employee WHERE city like "lethbridge";


## Invoice
9. Use the Invoice table for the following
* Count how many orders were made from the USA
    SELECT COUNT(*) FROM Invoice WHERE BillingCountry LIKE "usa"

* Find the largest order total amount
    SELECT * FROM Invoice ORDER BY total DESC LIMIT 1 //Total = 25.86

* Find the smallest order total amount
      SELECT * FROM Invoice ORDER BY total LIMIT 1 //Total = 0.99

* Find all orders bigger than $5
      SELECT * FROM Invoice WHERE total > 5

* Count how many orders were smaller than $5
      SELECT Count(*) FROM Invoice WHERE total < 5

* Count how many orders were in CA, TX, or AZ (use IN)
      SELECT Count(*) FROM Invoice WHERE billingState IN ("CA", "TX", "AZ") //35

* Get the average total of the orders
      SELECT AVG(total) FROM Invoice //5.65194...

* Get the total sum of the orders
      SELECT sum(total) FROM Invoice //2328.600000000004


## Copyright

© DevMountain LLC, 2016. Unauthorized use and/or duplication of this material without express and written permission from DevMountain, LLC is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to DevMountain with appropriate and specific direction to the original content.
