1757. Recyclable and Low Fat Products

Write an SQL query to find the ids of products that are both low fat and recyclable. Return the result table in any order. Table: Products

```sql
SELECT product_id FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```

1741. Find Total Time Spent by Each Employee

Write an SQL query to calculate the total time in minutes spent by each employee on each day at the office. Note that within one day, an employee can enter and leave more than once. The time spent in the office for a single entry is out_time - in_time. Return the result table in any order. Table: Employees

```sql
SELECT event_day AS day, emp_id, SUM(out_time - in_time) AS total_time FROM Employees
GROUP BY event_day, emp_id;
```

1693. Daily Leads and Partners

Write an SQL query that will, for each date_id and make_name, return the number of distinct lead_id's and distinct partner_id's. Return the result table in any order. Table: DailySales

```sql
SELECT date_id, make_name, COUNT(DISTINCT lead_id) AS unique_leads, COUNT(DISTINCT partner_id) AS unique_partners
FROM DailySales
GROUP BY date_id, make_name;
```
