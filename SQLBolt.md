#Table of Contents
[Main Page](https://github.com/Compsight/SQL-Fundamentals)<br><br>
[SELECT Basics](#select-basics)<br>

## SELECT Basics
[Back to Table of Contents](#table-of-contents)
* Using table (world) from: http://sqlzoo.net/wiki/SELECT_basics

* The example uses a WHERE clause to show the population of 'France'. Note that strings (pieces of text that are data) should be in 'single quotes';
Modify it to show the population of Germany

```
SELECT population FROM world
    WHERE name = 'Germany'
```

* Checking a list The word IN allows us to check if an item is in a list. The example shows the name and population for the countries 'Luxembourg', 'Mauritius' and 'Samoa'.
Show the name and the population for 'Ireland', 'Iceland' and 'Denmark'.

```
SELECT name, population FROM world
    WHERE name IN ('Ireland','Iceland','Denmark');
```

* Which countries are not too small and not too big? BETWEEN allows range checking (range specified is inclusive of boundary values). The example below shows countries with an area of 250,000-300,000 sq. km. Modify it to show the country and the area for countries with an area between 200,000 and 250,000.

```
SELECT name, area FROM world
    WHERE area BETWEEN 200000 AND 250000
```


* Using table (world) from: http://sqlzoo.net/wiki/SELECT_from_WORLD_Tutorial

## SELECT from WORLD Tutorial
[Back to Table of Contents](#table-of-contents)
* Read the notes about this table. Observe the result of running a simple SQL command.
```
SELECT name, continent, population FROM world
```
* How to use WHERE to filter records. Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

* Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

```
SELECT name, population/1000000 FROM world WHERE continent = 'South America'
```
* Show the name and population for France, Germany, Italy
