# SQLBolt

[SQLBolt](https://sqlbolt.com/lesson/select_queries_introduction) website

#Table of Contents
[Main Page](https://github.com/Compsight/SQL-Fundamentals)<br><br>
[SQL Lesson 1: SELECT queries 101](#sql-lesson-1-select-queries-101)<br>
[SQL Lesson 2: Queries with constraints (Pt. 1)](#sql-lesson-2-queries-with-constraints-pt-1)<br>
[SQL Lesson 3: Queries with constraints (Pt. 2)](#sql-lesson-3-queries-with-constraints-pt-2)<br>
[SQL Lesson 4: Filtering and sorting Query results](#sql-lesson-4-filtering-and-sorting-query-results)<br>
[SQL Review: Simple SELECT Queries](sql-review-simple-select-queries)<br>
[SQL Lesson 6: Multi-table queries with JOINs](#sql-lesson-6-multi-table-queries-with-joins)<br>
[SQL Lesson 7: OUTER JOINs](#sql-lesson-7-outer-joins)<br>
[SQL Lesson 8: A short note on NULLs](#sql-lesson-8-a-short-note-on-nulls)<br>
[SQL Lesson 9: Queries with expressions](#sql-lesson-9-queries-with-expressions)<br>
[SQL Lesson 10: Queries with aggregates (Pt. 1)](#sql-lesson-10-queries-with-aggregates-pt-1)<br>
[SQL Lesson 11: Queries with aggregates (Pt. 2)](#sql-lesson-11-queries-with-aggregates-pt-2)<br>
[SQL Lesson 12: Order of execution of a Query](#sql-lesson-12-order-of-execution-of-a-query)<br>
[SQL Lesson 13: Inserting rows](#sql-lesson-13-inserting-rows)<br>
[SQL Lesson 14: Updating rows](#sql-lesson-14-updating-rows)<br>
[SQL Lesson 15: Deleting rows](#sql-lesson-15-deleting-rows)<br>

## SQL Lesson 1: SELECT queries 101
[Back to Table of Contents](#table-of-contents)<br>
1\. Find the title of each film
```
SELECT Title FROM movies;
```

2\. Find the director of each film
```
SELECT Director FROM movies;
```

3\. Find the title and director of each film
```
SELECT Title, Director FROM movies;
```

4\. Find the title and year of each film
```
SELECT Title, Year FROM movies;
```

[]()5. Find all the information about each film
```
SELECT * FROM movies;
```

## SQL Lesson 2: Queries with constraints (Pt. 1)

1\. Find the movie with a row id of 6

```
SELECT * FROM movies
WHERE Id=6;
```

2\. Find the movies released in the years between 2000 and 2010

```
SELECT * FROM movies
WHERE Year BETWEEN 2000 AND 2010;
```

3\. Find the movies not released in the years between 2000 and 2010

```
SELECT * FROM movies
WHERE Year NOT BETWEEN 2000 AND 2010;
```

4\. Find the first 5 Pixar movies and their release year

```
SELECT * FROM movies LIMIT 5;
```

## SQL Lesson 3: Queries with constraints (Pt. 2)
1\. Find all the Toy Story movies
```
SELECT * FROM movies
WHERE Title LIKE 'Toy%';
```

2\. Find all the movies directed by John Lasseter
```
SELECT * FROM movies
WHERE Director='John Lasseter';
```

3\. Find all the movies (and director) not directed by John Lasseter
```
SELECT * FROM movies
WHERE NOT Director='John Lasseter';
```

4\. Find all the WALL-* movies
```
SELECT * FROM movies
WHERE Title LIKE 'WALL-%';
```

## SQL Lesson 4: Filtering and sorting Query results
1\. List all directors of Pixar movies (alphabetically), without duplicates
```
SELECT DISTINCT Director FROM movies
ORDER BY Director;
```

2\. List the last four Pixar movies released (ordered from most recent to least)
```
SELECT Title FROM movies
ORDER BY Year DESC LIMIT 4;
```

3\. List the first five Pixar movies sorted alphabetically
```
SELECT Title FROM movies
ORDER BY Title LIMIT 5;
```

4\. List the next five Pixar movies sorted alphabetically
```
SELECT Title FROM movies
ORDER BY Title LIMIT 5 OFFSET 5;
```

## SQL Review: Simple SELECT Queries
1\. List all the Canadian cities and their populations
```
SELECT * FROM north_american_cities
WHERE Country='Canada';
```

2\. Order all the cities in the United States by their latitude from north to south
```
SELECT * FROM north_american_cities
WHERE Country='United States' ORDER BY Latitude DESC;
```
3\. List all the cities west of Chicago, ordered from west to east
```
SELECT city, longitude FROM North_american_cities
WHERE Longitude < (SELECT longitude FROM North_american_cities WHERE city = "Chicago")
ORDER BY Longitude;
```

4\. List the two largest cities in Mexico (by population)
```
SELECT City FROM north_american_cities
WHERE Country='Mexico' ORDER BY Population DESC LIMIT 2;
```

[]()5. List the third and fourth largest cities (by population) in the United States and their population
```
SELECT City FROM north_american_cities
WHERE Country='United States'
ORDER BY Population DESC LIMIT 2 OFFSET 2;
```
## SQL Lesson 6: Multi-table queries with JOINs

1\. Find the domestic and international sales for each movie
```
SELECT Movies.title, Boxoffice.Domestic_sales, Boxoffice.International_sales FROM Movies
JOIN Boxoffice ON Movies.id = Boxoffice.Movie_id;
```

2\. Show the sales numbers for each movie that did better internationally rather than domestically
```
SELECT * FROM Movies
JOIN Boxoffice ON Id = Movie_id
WHERE International_sales > Domestic_sales;
```

3\. List all the movies by their ratings in descending order
```
SELECT * FROM Movies
JOIN Boxoffice ON Id = Movie_id
ORDER BY rating DESC;
```

## SQL Lesson 7: OUTER JOINs

1\. Find the list of all buildings that have employees
```
SELECT DISTINCT building FROM employees;
```

2\. Find the list of all buildings and their capacity
```
SELECT * FROM Buildings;
```

3\. List all buildings and the distinct employee roles in each building (including empty buildings)
```
SELECT DISTINCT Building_name, role FROM Buildings
LEFT JOIN Employees ON Building = Building_name;
```

## SQL Lesson 8: A short note on NULLs
1\. SELECT Name, Role FROM employees WHERE Building IS NULL;

2\. Find the names of the buildings that hold no employees
SELECT Building_name FROM buildings LEFT JOIN Employees ON Building_name=Building WHERE Building IS NULL;

## SQL Lesson 9: Queries with expressions

1\. List all movies and their combined sales in millions of dollars
 ```
SELECT '$'+ ROUND((Domestic_Sales + International_Sales)/1000000,2) AS Sales, *
FROM Movies
JOIN Boxoffice ON Id = Movie_id;

```

Alternate:
```
SELECT Title, ((Domestic_sales + International_sales) / 1000000) AS 'Millions of Dollars'
FROM movies
INNER JOIN boxoffice ON Id=Movie_id;
```

2\. List all movies and their ratings in percent

```
SELECT Title, (Rating*10) AS 'Percent' FROM movies INNER JOIN boxoffice ON Id=Movie_id;
```


3\. List all movies that were released on even number years
```
SELECT * FROM Movies
JOIN Boxoffice ON Movie_id = Id
WHERE Year % 2 = 0
```

## SQL Lesson 10: Queries with aggregates (Pt. 1)
1\. Find the longest time that an employee has been at the studio
```
SELECT MAX(Years_employed) FROM employees;
```

2\. For each role, find the average number of years employed by employees in that role
```
SELECT Role, AVG(Years_employed) FROM employees GROUP BY Role;
```

3\. Find the total number of employee years worked in each building
```
SELECT Building, SUM(Years_employed) FROM employees GROUP BY Building;
```


## SQL Lesson 11: Queries with aggregates (Pt. 2)
1\. Find the number of Artists in the studio (without a HAVING clause)
 ```
SELECT COUNT(Role) FROM employees WHERE Role='Artist';
```

2\. Find the number of Employees of each role in the studio
```
SELECT Role, COUNT(Role) FROM employees GROUP BY Role;
```

3\. Find the total number of years employed by all Engineers
```
SELECT Role, SUM(Years_employed) FROM employees GROUP BY Role HAVING Role='Engineer';
```


## SQL Lesson 12: Order of execution of a Query
1\. Find the number of movies each director has directed
```
SELECT Director, COUNT(Director) FROM movies GROUP BY Director;
```

2\. Find the total domestic and international sales that can be attributed to each director
```
SELECT Director, SUM(Domestic_sales + International_sales) AS 'Total Sales' FROM movies JOIN boxoffice ON Id=Movie_id GROUP BY Director;
```

## SQL Lesson 13: Inserting rows
1\. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
```
INSERT INTO movies (Title,Director,Year,Length_minutes) VALUES ('Toy Story 4','John Lasseter',2019,120);
```

2\. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table.
```
INSERT INTO boxoffice (Movie_id,Rating,Domestic_sales,International_sales) VALUES (15,8.7,340000000,270000000);
```


## SQL Lesson 14: Updating rows
1\. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter
```
UPDATE movies SET Director='John Lasseter' WHERE Id=2
```

2\. The year that Toy Story 2 was released is incorrect, it was actually released in 1999
```
UPDATE movies SET Year=1999 WHERE Title='Toy Story 2'
```

3\. Both the title and directory for Toy Story 8 is incorrect! The title should be "Toy Story 3"
```
UPDATE movies SET Title='Toy Story 3', Director='Lee Unkrich' WHERE Title='Toy Story 8'
```

## SQL Lesson 15: Deleting rows
1\. This database is getting too big, lets remove all movies that were released before 2005.
```
DELETE FROM movies WHERE Year<2005;
```

2\. Andrew Stanton has also left the studio, so please remove all movies directed by him.
```
DELETE FROM movies WHERE Director='Andrew Stanton';
```
