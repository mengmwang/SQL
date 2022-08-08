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

13. 
