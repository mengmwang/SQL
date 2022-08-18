**HackerRank Challenges - Medium**

1. Type of Triangle

Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table: 
- Equilateral: It's a triangle with 3 sides of equal length. 
- Isosceles: It's a triangle with 2 sides of equal length. 
- Scalene: It's a triangle with 3 sides of differing lengths. 
- Not A Triangle: The given values of A, B, and C don't form a triangle.
```sql
SELECT
CASE
WHEN (A+B>C AND B+C>A AND A+C>B) THEN
CASE
WHEN (A = B AND B = C) THEN 'Equilateral'
WHEN (A = B OR B = C OR A=C) THEN 'Isosceles'
ELSE 'Scalene'
END
ELSE 'Not A Triangle'
END
FROM TRIANGLES;
```

2. The PADS

Generate the following two result sets:
- Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
- Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format: There are a total of [occupation_count] [occupation]s. where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

Note: There will be at least two entries in the table for each type of occupation.
```sql
SELECT CONCAT(Name, '(', LEFT(Occupation,1), ')')
FROM OCCUPATIONS
ORDER BY Name ASC;
SELECT CONCAT('There are a total of ', COUNT(*), ' ', LOWER(Occupation),'s.')
FROM OCCUPATIONS
GROUP BY Occupation
ORDER BY COUNT(*) ASC, Occupation ASC;
```

3. Binary Tree Nodes

You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N. Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node: 
- Root: If node is root node. 
- Leaf: If node is leaf node. 
- Inner: If node is neither root nor leaf node.
```sql
SELECT N, 
CASE 
WHEN P IS NULL THEN 'Root'
WHEN N IN (SELECT P FROM BST) THEN 'Inner'
ELSE 'Leaf'
END
FROM BST
ORDER BY N;
```

4. Weather Observation Station 18

Consider p1(a,b) and p2(c,d) to be two points on a 2D plane. a happens to equal the minimum value in Northern Latitude (LAT_N in STATION). b happens to equal the minimum value in Western Longitude (LONG_W in STATION). c happens to equal the maximum value in Northern Latitude (LAT_N in STATION). d happens to equal the maximum value in Western Longitude (LONG_W in STATION). Query the Manhattan Distance between points p1 and p2 and round it to a scale of 4  decimal places.
```sql
SELECT ROUND(ABS(MAX(LAT_N) - MIN(LAT_N))+ ABS(MAX(LONG_W) - MIN(LONG_W)),4)
FROM STATION;
```

5. Weather Observation Station 19

Consider p1(a,c) and p2(b,d) to be two points on a 2D plane where (a,b) are the respective minimum and maximum values of Northern Latitude (LAT_N) and (c,d) are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION. Query the Euclidean Distance between points p1 and p2 and format your answer to display 4 decimal digits.
```sql
SELECT ROUND(POWER(POWER(MAX(LAT_N) - MIN(LAT_N),2)+ POWER(MAX(LONG_W) - MIN(LONG_W),2),0.5),4)
FROM STATION;
```

6. New Companies
Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy: Founder -> Lead Manager -> Senior Manager -> Manager -> Employee. Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.

Note: The tables may contain duplicate records. The company_code is string, so the sorting should not be numeric. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.

The following tables contain company data:
- Company: The company_code is the code of the company and founder is the founder of the company.
- Lead_Manager: The lead_manager_code is the code of the lead manager, and the company_code is the code of the working company.
- Senior_Manager: The senior_manager_code is the code of the senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.
- Manager: The manager_code is the code of the manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.
- Employee: The employee_code is the code of the employee, the manager_code is the code of its manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.
```sql
SELECT c.company_code, c.founder, COUNT(DISTINCT lm.lead_manager_code), COUNT(DISTINCT sm.senior_manager_code), COUNT(DISTINCT m.manager_code), COUNT(DISTINCT e.employee_code)
FROM Company AS c, Lead_Manager AS lm, Senior_Manager AS sm, Manager AS m, Employee AS e
WHERE c.company_code = lm.company_code AND lm.lead_manager_code = sm.lead_manager_code AND sm.senior_manager_code = m.senior_manager_code AND m.manager_code = e.manager_code
GROUP BY c.company_code, c.founder;
```

7. The Report

You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks. Grades contains the following data: Grade, Min_Mark, Max_Mark. Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade 

-- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order. Write a query to help Eve.
```sql
SELECT IF(g.grade<8, NULL, s.Name), g.Grade, s.Marks
FROM Students AS s
JOIN Grades AS g ON s.marks BETWEEN g.Min_Mark AND g.Max_Mark
ORDER BY g.Grade DESC, s.Name;
```

8. Top Competitors

Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

The following tables contain contest data: 
- Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker. 
- Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level. 
- Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge. 
- Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.
```sql
SELECT s.hacker_id, h.name
FROM Submissions AS s
JOIN Hackers AS h ON h.hacker_id = s.hacker_id
JOIN Challenges AS c ON c.challenge_id = s.challenge_id
JOIN Difficulty AS d ON d.difficulty_level = c.difficulty_level
WHERE s.score = d.score
GROUP BY s.hacker_id, h.name
HAVING COUNT(*)>1
ORDER BY COUNT(*) DESC, s.hacker_id;
```

9. Placements

You are given three tables: Students, Friends and Packages. Students contains two columns: ID and Name. Friends contains two columns: ID and Friend_ID (ID of the ONLY best friend). Packages contains two columns: ID and Salary (offered salary in $ thousands per month). Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.

```sql
SELECT s.Name FROM Students AS s
JOIN Friends AS f ON f.ID = S.ID
JOIN Packages AS p ON p.ID = s.ID
JOIN Packages AS p1 ON p1.ID = f.Friend_ID
WHERE p1.Salary > p.Salary
ORDER BY p1.Salary;
```
