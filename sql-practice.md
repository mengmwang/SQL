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

6. Show first name and last name concatinated into one column to show their full name.
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
**Medium Level**

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


