## SQL Challenges on [sql-practice](https://www.sql-practice.com/)

Databases: patients, admissions, physicians, medications, nursing_units, vendors, items, unit_dose_orders, provinces

**Easy level (13 questions)**

1. Show first name, last name, and gender of patients who's gender is 'M'
```sql
SELECT first_name, last_name, gender FROM patients
WHERE gender='M';
```

2. Show first name and last name of patients who does not have allergies (null).
```sql
SELECT first_name, last_name FROM patients
WHERE allergies IS NULL;
```

3. Show first name of patients that start with the letter 'C'
```sql
SELECT first_name FROM patients
WHERE first_name LIKE 'C%';
```

4. Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)
```sql
SELECT first_name, last_name FROM patients
WHERE weight BETWEEN 100 AND 120;
```

5. Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'
```sql
UPDATE patients
SET allergies='NKA'
WHERE allergies IS NULL;
```

6. Show first name and last name concatenated into one column to show their full name.
```sql
SELECT CONCAT(first_name, ' ', last_name)
FROM patients;
```

7. Show first name, last name, and the full province name of each patient. Example: 'Ontario' instead of 'ON'
```sql
SELECT first_name, last_name, (SELECT province_name FROM provinces WHERE provinces.province_id = patients.province_id)
FROM patients;
```
Another solution
```sql
SELECT first_name, last_name, province_name
FROM patients
JOIN provinces ON provinces.province_id = patients.province_id;
```

8. Show how many patients have a birth_date with 2010 as the birth year. 
```sql
SELECT COUNT() AS patient_2010
FROM patients
WHERE YEAR(birth_date)=2010;
```

9. Show the first_name, last_name, and height of the patient with the greatest height.
```sql
SELECT first_name, last_name, MAX(height) AS height
FROM patients;
```

10. Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000
```sql
SELECT * FROM patients
WHERE patient_id IN (1,45,534,879,1000);
```

11. Show the total number of admissions
```sql
SELECT COUNT(*) AS total_admission 
FROM admissions;
```

12. Show all the columns from admissions where the patient was admitted and discharged on the same day.
```sql
SELECT *
FROM admissions
WHERE admission_date=discharge_date;
```

13. Show the total number of admissions for patient_id 573.
```sql
SELECT patient_id, COUNT() AS admission_573
FROM admissions
WHERE patient_id=573;
```
**Medium Level (20 questions)**

1. Show unique birth years from patients and order them by ascending.
```sql
SELECT DISTINCT YEAR(birth_date)
FROM patients
ORDER BY YEAR(birth_date) ASC;
```

2. Show unique first names from the patients table which only occurs once in the list. For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.
```sql
SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(first_name)=1;
```

3. Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
```sql
SELECT patient_id, first_name
FROM patients
WHERE first_name LIKE 's____%s';
```

4. Show patient_id, first_name, last_name from patients whos primary_diagnosis is 'Dementia'. Primary diagnosis is stored in the admissions table.
```sql
SELECT patients.patient_id, first_name, last_name
FROM patients
JOIN admissions ON admissions.patient_id = patients.patient_id
WHERE admissions.primary_diagnosis = 'Dementia';
```
Another solution
```sql
SELECT patient_id, first_name, last_name
FROM patients
WHERE patient_id IN (
SELECT patient_id
FROM admissions
WHERE primary_diagnosis = 'Dementia');
```

5. Display every patient's first_name. Order the list by the length of each name and then by alphbetically
```sql
SELECT first_name FROM patients
ORDER BY LEN(first_name), first_name;
```

6. Show the total amount of male patients and the total amount of female patients in the patients table
```sql
SELECT 
COUNT(CASE WHEN gender = 'M' THEN 1 END) AS male_count,
COUNT(CASE WHEN gender = 'F' THEN 1 END) AS female_count 
SELECT patients;
```

Another solution
```sql
SELECT
(SELECT COUNT(gender) FROM patients WHERE gender='M') AS male_count,
(SELECT COUNT(gender) FROM patients WHERE gender='F') AS female_count;
```

7. Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.
```sql
SELECT first_name, last_name, allergies
FROM patients
WHERE allergies IN ('Penicillin', 'Morphine')
ORDER BY allergies ASC, first_name ASC, last_name ASC;
```

8. Show patient_id, primary_diagnosis from admissions. Find patients admitted multiple times for the same primary_diagnosis.
```sql
SELECT patient_id, primary_diagnosis
FROM admissions
GROUP BY patient_id, primary_diagnosis
Having Count(primary_diagnosis)>1;
```

9. Show the city and the total number of patients in the city in the order from most to least patients.
```sql
SELECT city, COUNT(*) AS num_patients
FROM patients
GROUP BY city
ORDER BY COUNT(*) DESC;
```

10. Show first name, last name and role of every person that is either patient or physician. The roles are either "Patient" or "Physician"
```sql
SELECT first_name, last_name, 'Patient' AS Role
FROM patients
UNION
SELECT first_name, last_name, 'Physician'
FROM physicians;
```

11. Show all allergies ordered by popularity. Remove 'NKA' and NULL values from query.
```sql
SELECT allergies, COUNT(*) 
FROM patients
WHERE allergies IS NOT NULL AND allergies <> 'NKA'
GROUP BY allergies
ORDER BY COUNT(*) DESC;
```

12. Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.
```sql
SELECT first_name, last_name, birth_date
FROM patients
WHERE YEAR(birth_date)>=1970 AND YEAR(birth_date)<=1979
ORDER BY birth_date;
```

13. We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order. EX: SMITH,jane
```sql
SELECT CONCAT(UPPER(last_name), ',', LOWER(first_name))
FROM patients
ORDER BY first_name DESC;
```

14. Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.
```sql
SELECT province_id, SUM(height)
FROM patients
GROUP BY province_id
HAVING SUM(height)>=7000;
```

15. Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'
```sql
SELECT (MAX(weight)-MIN(weight)) AS diffweight
FROM patients
WHERE last_name='Maroni';
```

16. Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?
```sql
SELECT DISTINCT city AS unique_cities
FROM patients
WHERE proviNce_id='NS';
```

17. Show all of the month's day numbers and how many admission_dates occurred on that number. Sort by the day with most admissions to least admissions.
```sql
SELECT DAY(admission_date) AS day_number, COUNT(*) AS admission_number
FROM admissions
GROUP BY DAY(admission_date)
ORDER BY COUNT(*) DESC;
```

18. Show the patient_id, nursing_unit_id, room, and bed for patient_id 542's most recent admission_date.
```sql
SELECT patient_id, nursing_unit_id, room, bed
FROM admissions
WHERE patient_id=542
ORDER BY admission_date DESC
LIMIT 1;
```

19. Show the nursing_unit_id and count of admissions for each nursing_unit_id. Exclude the following nursing_unit_ids: 'CCU', 'OR', 'ICU', 'ER'.
```sql
SELECT nursing_unit_id, COUNT(*) AS total_admissions
FROM admissions
GROUP BY nursing_unit_id
HAVING nursing_unit_id NOT IN ('CCU', 'OR', 'ICU', 'ER');
```

20. Show patient_id, attending_physician_id, and primary_diagnosis for admissions that match one of the two criteria: 1. patient_id is an odd number and attending_physician_id is either 1, 5, or 19. 2. attending_physician_id contains a 2 and the length of patient_id is 3 characters.
```sql
SELECT patient_id, attending_physician_id, primary_diagnosis
FROM admissions
WHERE (patient_id %2 <> 0 AND attending_physician_id IN (1,5,19))
OR (attending_physician_id LIKE '%2%' AND LEN(patient_id)=3);
``` 

**Hard Level (10 questions)**
1. Show all of the patients grouped into weight groups. Show the total amount of patients in each weight group. Order the list by the weight group decending. For example, if they weight 100 to 109 they are placed in the 100 weight group, 110-119 = 110 weight group, etc.
```sql
SELECT COUNT(*) AS patient_in_group, FLOOR(weight/10)*10 AS weight_group
FROM patients
GROUP BY weight_group
ORDER BY weight_group DESC;
```

2. Show patient_id, weight, height, isObese from the patients table. Display isObese as a boolean 0 or 1. Obese is defined as weight(kg)/(height(m)2) >= 30. weight is in units kg. height is in units cm.
```sql
SELECT patient_id, weight, height,
CASE
    WHEN (weight/(POWER(height/100.0,2))) >=30 THEN 1
    ELSE 0
END AS isObese
FROM patients;
```

3. Show patient_id, first_name, last_name, and attending physician's specialty. Show only the patients who has a primary_diagnosis as 'Dementia' and the physician's first name is 'Lisa' Check patients, admissions, and physicians tables for required information.
```sql
SELECT patients.patient_id, patients.first_name, patients.last_name, physicians.specialty
FROM patients
JOIN admissions ON patients.patient_id = admissions.patient_id
JOIN physicians ON admissions.attending_physician_id = 	physicians.physician_id
WHERE admissions.primary_diagnosis = 'Dementia' AND physicians.first_name = 'Lisa';
```

Another solution
```sql
SELECT
  a.patient_id,
  a.first_name,
  a.last_name,
  b.specialty
FROM
  patients a,
  physicians b,
  admissions c
WHERE
  a.patient_id = c.patient_id
  AND c.attending_physician_id = b.physician_id
  AND c.primary_diagnosis = 'Dementia'
  AND b.first_name = 'Lisa';
  ```

4. All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password. The password must be the following, in order: 1. patient_id 2. the numerical length of patient's last_name 3. year of patient's birth_date
```sql
SELECT DISTINCT p.patient_id, CONCAT(p.patient_id, LEN(p.last_name), YEAR(p.birth_date)) AS temp_password
FROM patients AS p, admissions AS a
WHERE a.patient_id = p.patient_id;
```

Another solution
```sql
SELECT
  DISTINCT P.patient_id,
  CONCAT(
    P.patient_id,
    LEN(last_name),
    YEAR(birth_date)
  ) AS temp_password
FROM patients P
  JOIN admissions A ON A.patient_id = P.patient_id;
```

5. Each admission costs $50 for patients without insurance, and $10 for patients with insurance. All patients with an even patient_id have insurance. Give each patient a 'Yes' if they have insurance, and a 'No' if they don't have insurance. Add up the admission_total cost for each has_insurance group.
```sql
SELECT
CASE
WHEN patient_id %2 = 0 THEN 'Yes'
ELSE 'No'
END AS has_insurance, 
SUM(
CASE 
WHEN patient_id %2 = 0 THEN 10
ELSE 50 
END) AS cost 
FROM admissions
GROUP BY has_insurance;
```

Another solution
```sql
SELECT 'No' AS has_insurance, COUNT(*) * 50 AS cost
FROM admissions WHERE patient_id % 2 = 1 GROUP BY has_insurance
UNION
SELECT 'Yes' AS has_insurance, COUNT(*) * 10 AS cost
FROM admissions WHERE patient_id % 2 = 0 GROUP BY has_insurance
```

6. Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name
```sql
SELECT province_name
FROM provinces
JOIN patients ON provinces.province_id = patients.province_id
GROUP BY provinces.province_name
HAVING
(SUM(CASE WHEN patients.gender='M' THEN 1 ELSE 0 END)) > (SUM(CASE WHEN patients.gender='F' THEN 1 ELSE 0 END));
```

7. We are looking for a specific patient. Pull all columns for the patient who matches the following criteria: - First_name contains an 'r' after the first two letters. - Identifies their gender as 'F' - Born in February, May, or December - Their weight would be between 60kg and 80kg - Their patient_id is an odd number - They are from the city 'Halifax'
```sql
SELECT * FROM patients
WHERE first_name LIKE '__r%'
AND gender='F'
AND MONTH(birth_date) IN (2,5,12)
AND weight BETWEEN 60 AND 80
AND patient_id %2 = 1
AND city = 'Halifax';
```

8. Show the percent of patients that have 'M' as their gender. Round the answer to the nearest hundreth number and in percent form.
```sql
SELECT 
CONCAT(ROUND(100.0*SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END)/COUNT(*),2),'%') AS male_precent
FROM patients;
--solution
SELECT 
   CONCAT(ROUND(SUM(gender='M') / CAST(COUNT(*) AS FLOAT), 4) * 100, '%')
FROM patients;
```

9. Show the patient_id and total_spent for patients who spent over 150 in combined medication_cost. Sort by most total_spent to least total_spent.
```sql
SELECT u.patient_id, 
SUM(m.medication_cost) AS total_spent
FROM unit_dose_orders AS u
JOIN medications AS m ON u.medication_id = m.medication_id
GROUP BY u.patient_id
HAVING total_spent > 150
ORDER BY total_spent DESC;
```

10. Provide the description of each item, along with the total cost of the quantity on hand (rounded to the nearest whole dollar), and the associated primary vendor. Sort the output by the most spent to the least spent on inventory.
```sql
SELECT i.item_description, ROUND(i.quantity_on_hand*i.item_cost,0) AS total_cost, v.vendor_name
FROM items AS i
JOIN vendors AS v ON v.vendor_id = i.primary_vendor_id
ORDER BY total_cost DESC, i.item_description DESC;
```

