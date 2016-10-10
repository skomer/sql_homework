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

  2. Select the names of all shows that cost less than £15.

  3. Insert a user with the name "Val Gibson" into the users table.

  4. Insert a record that Val Gibson wants to attend the show "Two girls, one cup of comedy".

  5. Updates the name of the "Val Gibson" user to be "Valerie Gibson".

  6. Deletes the user with the name 'Valerie Gibson'.

  7. Deletes the shows for the user you just deleted.


## Section 2

  This section involves more complex queries.  You will need to go and find out about aggregate funcions in SQL to answer some of the next questions.

  9. Select the names and prices of all shows, ordered by price in ascending order.

  10. Select the average price of all shows.

  11. Select the price of the least expensive show.

  12. Select the sum of the price of all shows.

  13. Select the sum of the price of all shows whose prices is less than £20.

  14. Select the name and price of the most expensive show.

  15. Select the name and price of the second from cheapest show.

  16. Select the names of all users whose names start with the letter "N".

  17. Select the names of users whose names contain "er".


## Section 3

  The following questions can be answered by using nested SQL statements but ideally you should learn about JOIN clauses to answer them.

  18. Select the time for the Edinburgh Royal Tattoo.

  19. Select the number of users who want to see "Shitfaced Shakespeare".

  20. Select all of the user names and the count of shows they're going to see.

  21. SELECT all users who are going to a show at 17:15.
