## SQL Questions

First create a database called fringe_shows
```
  #terminal
  psql
  create database fringe_shows;
  \q
```

Populate the data using the script - fringeshows.sql
```
  #terminal
  psql -d fringe_shows -f fringeshows.sql
```

Using the SQL Database file given to you as the source of data to answer the questions.  Copy the SQL command you have used to get the answer, and paste it below the question, along with the result they gave.


## Section 1

  Revision of concepts that we've learnt in SQL today

  1. Select the names of all users.
  
  SELECT name FROM users;

             name
  ---------------------------
   Keith Douglas
   Craig Morton
   Sandy McMillan
   Adrian Tuckwell
   Alex Bazlinton
   Bertie Coll
   Bobby Ross
   Carlos Pereira
   Claudia Menting
   Cookie Lacson
   Cyrus Balsara
   David OLeary
   Diana Man
   Euan Ramsay
   Josephine Elder
   Kate Manson
   Kyle Grenell
   Matthew Jeorrett
   Max Veasey
   Paul Milne
   Pavlos MacDonald-Kosmidis
   Ross Loggie
   Thomas Crines
   Tom Benham
  (24 rows)


  2. Select the names of all shows that cost less than £15.
  
  SELECT name FROM shows WHERE price < 15;

               name
  ------------------------------
   Le Haggis
   Paul Dabek Mischief
   Best of Burlesque
   Two become One
   Urinetown
   Two girls, one cup of comedy
  (6 rows)


  3. Insert a user with the name "Val Gibson" into the users table.
  
  INSERT INTO users (name) VALUES ('Val Gibson');

  INSERT 0 1


  4. Insert a record that Val Gibson wants to attend the show "Two girls, one cup of comedy".
  
  INSERT INTO shows_users (show_id, user_id)
  VALUES ((SELECT id
    FROM shows
    WHERE name = 'Two girls, one cup of comedy'),
  (SELECT id
    FROM users
    WHERE name = 'Val Gibson'));

  INSERT 0 1


  5. Updates the name of the "Val Gibson" user to be "Valerie Gibson".
  
  UPDATE users SET name = 'Valerie Gibson' WHERE name = 'Val Gibson';

  UPDATE 1


  6. Deletes the user with the name 'Valerie Gibson'.
  
  DELETE FROM users WHERE name = 'Valerie Gibson';

  DELETE 1


  7. Deletes the shows for the user you just deleted.
  I got confused with this one


## Section 2

  This section involves more complex queries.  You will need to go and find out about aggregate funcions in SQL to answer some of the next questions.


  9. Select the names and prices of all shows, ordered by price in ascending order.
  
  SELECT name, price FROM shows ORDER BY price ASC;

                    name                   | price
  -----------------------------------------+-------
   Two girls, one cup of comedy            |  6.00
   Best of Burlesque                       |  7.99
   Two become One                          |  8.50
   Urinetown                               |  8.50
   Paul Dabek Mischief                     | 12.99
   Le Haggis                               | 12.99
   Joe Stilgoe: Songs on Film – The Sequel | 16.50
   Game of Thrones - The Musical           | 16.50
   Shitfaced Shakespeare                   | 16.50
   Aaabeduation – A Magic Show             | 17.99
   Camille O'Sullivan                      | 17.99
   Balletronics                            | 32.00
   Edinburgh Royal Tattoo                  | 32.99
  (13 rows)


  10. Select the average price of all shows.
  
  SELECT AVG(price) FROM shows;

           avg
  ---------------------
   15.9569230769230769
  (1 row)


  11. Select the price of the least expensive show.
 
  SELECT MIN(price) FROM shows;

   min
  ------
   6.00
  (1 row)


  12. Select the sum of the price of all shows.
  
  SELECT SUM(price) FROM shows;

    sum
  --------
   207.44
  (1 row)


  13. Select the sum of the price of all shows whose prices is less than £20.
  
  SELECT SUM(price) FROM shows WHERE price < 20;

    sum
  --------
   142.45
  (1 row)


  14. Select the name and price of the most expensive show.
  
  SELECT name, price
  FROM shows
  ORDER BY price DESC
  LIMIT 1;

            name          | price
  ------------------------+-------
   Edinburgh Royal Tattoo | 32.99
  (1 row)


  15. Select the name and price of the second from cheapest show.
  
  CREATE VIEW two_cheapest_shows AS
  SELECT name, price
  FROM shows
  ORDER BY price ASC
  LIMIT 2;
  SELECT name, price
  FROM two_cheapest_shows
  ORDER BY price DESC
  LIMIT 1;

         name        | price
  -------------------+-------
   Best of Burlesque |  7.99
  (1 row)


  16. Select the names of all users whose names start with the letter "N".
  
  SELECT name FROM users WHERE name LIKE 'N%';

   name
  ------
  (0 rows)


  17. Select the names of users whose names contain "er".
  
  SELECT name FROM users WHERE name LIKE '%er%';

        name
  -----------------
   Bertie Coll
   Carlos Pereira
   Josephine Elder
  (3 rows)



## Section 3

  The following questions can be answered by using nested SQL statements but ideally you should learn about JOIN clauses to answer them.


  18. Select the time for the Edinburgh Royal Tattoo.

  SELECT times.time
  FROM times
  INNER JOIN shows
  ON times.show_id = shows.id
  WHERE shows.name = 'Edinburgh Royal Tattoo';

   time
  -------
   22:00
  (1 row)


  19. Select the number of users who want to see "Shitfaced Shakespeare".

  SELECT COUNT(shows_users.user_id)
  FROM shows_users
  INNER JOIN shows
  ON shows_users.show_id = shows.id
  WHERE shows.name = 'Shitfaced Shakespeare';

   count
  -------
       7
  (1 row)


  20. Select all of the user names and the count of shows they're going to see.
  
  SELECT (users.name, COUNT(shows_users.show_id))
  FROM shows_users
  INNER JOIN users
  ON shows_users.user_id = users.id
  GROUP BY users.name;

                 row
  ---------------------------------
   ("Carlos Pereira",5)
   ("Alex Bazlinton",4)
   ("Bertie Coll",4)
   ("Pavlos MacDonald-Kosmidis",1)
   ("Josephine Elder",7)
   ("Bobby Ross",4)
   ("Claudia Menting",7)
   ("David OLeary",6)
   ("Keith Douglas",5)
   ("Sandy McMillan",6)
   ("Max Veasey",1)
   ("Paul Milne",1)
   ("Kyle Grenell",1)
   ("Cookie Lacson",6)
   ("Adrian Tuckwell",4)
   ("Craig Morton",5)
   ("Euan Ramsay",8)
   ("Diana Man",5)
   ("Matthew Jeorrett",1)
   ("Cyrus Balsara",5)
  (20 rows)



  21. SELECT all users who are going to a show at 17:15.
  
  SELECT users.name
  FROM shows_users
  INNER JOIN users
  ON shows_users.user_id = users.id
  INNER JOIN times
  ON shows_users.show_id = times.show_id
  WHERE times.time = '17:15';
  
        name
  -----------------
   Keith Douglas
   Sandy McMillan
   Alex Bazlinton
   Carlos Pereira
   Claudia Menting
   Diana Man
   Josephine Elder
   Cyrus Balsara
   David OLeary
   Diana Man
   Cookie Lacson
   Euan Ramsay
  (12 rows)
