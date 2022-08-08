HackerRank Challenges - Easy

1. Revising the Select Query I

Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.
```sql
SELECT * FROM CITY
WHERE COUNTRYCODE='USA' AND POPULATION>100000;
```

2. Revising the Select Query II

Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.
```sql
SELECT NAME FROM CITY
WHERE COUNTRYCODE='USA' AND POPULATION>120000;
```

3. Select All

Query all columns (attributes) for every row in the CITY table.
```sql
SELECT * FROM CITY;
```

4. Select By ID

Query all columns for a city in CITY with the ID 1661.
```sql
SELECT * FROM CITY
WHERE ID=1661;
```

5. Japanese Cities' Attributes

Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.
```sql
SELECT * FROM CITY
WHERE COUNTRYCODE='JPN';
```

6. Japanese Cities' Names

Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.
```sql
SELECT NAME FROM CITY
WHERE COUNTRYCODE='JPN';
```

7. Revising Aggregations - The Count Function

Query a count of the number of cities in CITY having a Population larger than 100,000.
```sql
SELECT COUNT(*) FROM CITY
WHERE POPULATION>100000;
```

8. Revising Aggregations - The Sum Function

Query the total population of all cities in CITY where District is California.
```sql
SELECT SUM(POPULATION) FROM CITY
WHERE DISTRICT='California';
```

9. Revising Aggregations - Averages

Query the average population of all cities in CITY where District is California.
```sql
SELECT AVG(POPULATION) FROM CITY
WHERE DISTRICT='California';
```

10. Average Population

Query the average population for all cities in CITY, rounded down to the nearest integer.
```sql
SELECT ROUND(AVG(POPULATION),0) FROM CITY;
```

11. Japan Population

Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.
```sql
SELECT SUM(POPULATION) FROM CITY
WHERE COUNTRYCODE='JPN';
```

12. Population Density Difference

Query the difference between the maximum and minimum populations in CITY.
```sql
SELECT MAX(POPULATION)-MIN(POPULATION) FROM CITY;
```

13. Weather Observation Station 1

Query a list of CITY and STATE from the STATION table.
```sql
SELECT CITY, STATE FROM STATION;
```

14. Weather Observation Station 2

Query the following two values from the STATION table:
1. The sum of all values in LAT_N rounded to a scale of 2 decimal places.
2. The sum of all values in LONG_W rounded to a scale of 2 decimal places.
```sql
SELECT ROUND(SUM(LAT_N),2), ROUND(SUM(LONG_W),2)
FROM STATION;
```

15. Weather Observation Station 3

Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.
```sql
SELECT DISTINCT CITY FROM STATION
WHERE ID%2=0;
```

16. Weather Observation Station 4

Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.
```sql
SELECT COUNT(CITY)-COUNT(DISTINCT CITY) AS CITYNUM
FROM STATION;
```

17. Weather Observation Station 5

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
```sql
(SELECT CITY, LENGTH(CITY) FROM STATION
ORDER BY LENGTH(CITY), CITY
LIMIT 1)
UNION
(SELECT CITY, LENGTH(CITY) FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY
LIMIT 1);
```

18. Weather Observation Station 6

Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.
```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY LIKE 'a%' OR CITY LIKE 'e%' OR CITY LIKE 'i%' OR CITY LIKE 'o%' OR CITY LIKE 'u%';
```

19. Weather Observation Station 7

Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.
```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY LIKE '%a' OR CITY LIKE '%e' OR CITY LIKE '%i' OR CITY LIKE '%o' OR CITY LIKE '%u';
```

20. Weather Observation Station 8

Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.
```sql
SELECT DISTINCT CITY FROM STATION
WHERE LEFT(CITY,1) IN ('a','e','i','o','u') AND RIGHT(CITY,1) IN ('a','e','i','o','u');
```

21. Weather Observation Station 9

Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.
```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY NOT LIKE 'a%' AND CITY NOT LIKE 'e%' AND CITY NOT LIKE 'i%' AND CITY NOT LIKE 'o%' AND CITY NOT LIKE 'u%';
```

22. Weather Observation Station 10

Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.
```sql
SELECT DISTINCT CITY FROM STATION
WHERE RIGHT(CITY,1) NOT IN ('a','e','i','o','u');
```

23. Weather Observation Station 11

Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.
```sql
SELECT DISTINCT CITY FROM STATION
WHERE LEFT(CITY,1) NOT IN ('a','e','i','o','u') OR RIGHT(CITY,1) NOT IN ('a','e','i','o','u');
```

24. Weather Observation Station 12

Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.
```sql
SELECT DISTINCT CITY FROM STATION
WHERE LEFT(CITY,1) NOT IN ('a','e','i','o','u') AND RIGHT(CITY,1) NOT IN ('a','e','i','o','u');
```

25. Weather Observation Station 13

Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880 and less than 137.2345. Truncate your answer to 4 decimal places.
```sql
SELECT ROUND(SUM(LAT_N),4)
FROM STATION
WHERE LAT_N BETWEEN 38.7880 AND 137.2345;
```

26. Weather Observation Station 14

Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345. Truncate your answer to 4 decimal places.
```sql
SELECT ROUND(LAT_N,4)
FROM STATION
WHERE LAT_N<137.2345
ORDER BY LAT_N DESC
LIMIT 1;
```

27. Weather Observation Station 15

Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Round your answer to 4 decimal places.
```sql
SELECT ROUND(LONG_W,4) FROM STATION
WHERE LAT_N<137.2345
ORDER BY LAT_N DESC
LIMIT 1;
```

28. Weather Observation Station 16

Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.7780. Round your answer to 4 decimal places.
```sql
SELECT ROUND(LAT_N,4) FROM STATION
WHERE LAT_N>38.7780
ORDER BY LAT_N ASC
LIMIT 1;
```

29. Weather Observation Station 17

Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7780. Round your answer to 4 decimal places.
```sql
SELECT ROUND(LONG_W,4) FROM STATION
WHERE LAT_N>38.7780
ORDER BY LAT_N ASC
LIMIT 1;
```


