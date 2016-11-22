# SQLBolt

[SQLBolt](https://sqlbolt.com/lesson/select_queries_introduction) website

#Table of Contents
[Main Page](https://github.com/Compsight/SQL-Fundamentals)<br><br>
[SQL Lesson 1: SELECT queries 101](#sql-lesson-1-select-queries-101)<br>
[SQL Lesson 2: Queries with constraints (Pt. 1)](#sql-lesson-2-queries-with-constraints-pt-1)
[SQL Lesson 3: Queries with constraints (Pt. 2)](#sql-lesson-3-queries-with-constraints-pt-2)
[SQL Lesson 4: Filtering and sorting Query results](#sql-lesson-4-filtering-and-sorting-query-results)
[SQL Review: Simple SELECT Queries](sql-review-simple-select-queries)
[SQL Lesson 6: Multi-table queries with JOINs](#sql-lesson-6-multi-table-queries-with-joins)

## SQL Lesson 1: SELECT queries 101
[Back to Table of Contents](#table-of-contents)<br>
[]()1. Find the title of each film
```
SELECT Title FROM movies;
```

[]()2. Find the director of each film
```
SELECT Director FROM movies;
```

[]()3. Find the title and director of each film
```
SELECT Title, Director FROM movies;
```

[]()4. Find the title and year of each film
```
SELECT Title, Year FROM movies;
```

[]()5. Find all the information about each film
```
SELECT * FROM movies;
```

## SQL Lesson 2: Queries with constraints (Pt. 1)

[]()1. Find the movie with a row id of 6

```
SELECT * FROM movies WHERE Id=6;
```

[]()2. Find the movies released in the years between 2000 and 2010

```
SELECT * FROM movies WHERE Year BETWEEN 2000 AND 2010;
```

[]()3. Find the movies not released in the years between 2000 and 2010

```
SELECT * FROM movies WHERE Year NOT BETWEEN 2000 AND 2010;
```

[]()4. Find the first 5 Pixar movies and their release year

```
SELECT * FROM movies LIMIT 5;
```

## SQL Lesson 3: Queries with constraints (Pt. 2)
[]()1. Find all the Toy Story movies
```
SELECT * FROM movies WHERE Title LIKE 'Toy%';
```

[]()2. Find all the movies directed by John Lasseter
```
SELECT * FROM movies WHERE Director='John Lasseter';
```

[]()3. Find all the movies (and director) not directed by John Lasseter
```
SELECT * FROM movies WHERE NOT Director='John Lasseter';
```

[]()4. Find all the WALL-* movies
```
SELECT * FROM movies WHERE Title LIKE 'WALL-%';
```

## SQL Lesson 4: Filtering and sorting Query results
[]()1. List all directors of Pixar movies (alphabetically), without duplicates
```
SELECT DISTINCT Director FROM movies ORDER BY Director;
```

[]()2. List the last four Pixar movies released (ordered from most recent to least)
```
SELECT Title FROM movies ORDER BY Year DESC LIMIT 4;
```

[]()3. List the first five Pixar movies sorted alphabetically
```
SELECT Title FROM movies ORDER BY Title LIMIT 5;
```

[]()4. List the next five Pixar movies sorted alphabetically
```
SELECT Title FROM movies ORDER BY Title LIMIT 5 OFFSET 5;
```

## SQL Review: Simple SELECT Queries
[]()1. List all the Canadian cities and their populations
```
SELECT * FROM north_american_cities WHERE Country='Canada';
```
[]()2. Order all the cities in the United States by their latitude from north to south
```
SELECT * FROM north_american_cities WHERE Country='United States' ORDER BY Latitude DESC;
```
[]()3. List all the cities west of Chicago, ordered from west to east
```
SELECT city, longitude FROM North_american_cities WHERE
Longitude < (SELECT longitude FROM North_american_cities WHERE city = "Chicago")
ORDER BY Longitude
```
[]()4. List the two largest cities in Mexico (by population)
```
SELECT City FROM north_american_cities WHERE Country='Mexico' ORDER BY Population DESC LIMIT 2
```
[]()5. List the third and fourth largest cities (by population) in the United States and their population
```
SELECT City FROM north_american_cities WHERE Country='United States' ORDER BY Population DESC LIMIT 2 OFFSET 2
```
## SQL Lesson 6: Multi-table queries with JOINs

[]()1. Find the domestic and international sales for each movie
```
SELECT Movies.title, Boxoffice.Domestic_sales, Boxoffice.International_sales FROM Movies
JOIN Boxoffice ON Movies.id = Boxoffice.Movie_id;
```

[]()2. Show the sales numbers for each movie that did better internationally rather than domestically
```
SELECT * FROM Movies
JOIN Boxoffice ON Id = Movie_id
WHERE International_sales > Domestic_sales
```
[]()3. List all the movies by their ratings in descending order
```
SELECT * FROM Movies
JOIN Boxoffice ON Id = Movie_id
ORDER BY rating DESC
```
