**Practice SQL on [sql-practice](https://www.sql-practice.com/)**

Databases: patients, admissions, physicians, medications, nursing_units, vendors, items, unit_dose_orders, provinces

Easy level (13 questions)

1. Show first name, last name, and gender of patients who's gender is 'M'
``` sql
SELECT first_name, last_name, gender FROM patients
WHERE gender='M';
```

2. Show first name and last name of patients who does not have allergies (null).
``` sql
SELECT first_name, last_name FROM patients
WHERE allergies IS NULL;
```

3. Show first name of patients that start with the letter 'C'
``` sql
SELECT first_name FROM patients
WHERE first_name LIKE 'C%';
```

4. Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)
``` sql
SELECT first_name, last_name FROM patients
WHERE weight BETWEEN 100 AND 120;
```

5. Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'
``` sql
UPDATE patients
SET allergies='NKA'
WHERE allergies IS NULL;
```

6. Show first name and last name concatinated into one column to show their full name.
``` sql
SELECT CONCAT(first_name, ' ', last_name)
FROM patients;
```

7. Show first name, last name, and the full province name of each patient. Example: 'Ontario' instead of 'ON'
``` sql
SELECT first_name, last_name, (SELECT province_name FROM provinces WHERE provinces.province_id = patients.province_id)
FROM patients;
```
Another solution
``` sql
SELECT first_name, last_name, province_name
FROM patients
JOIN provinces ON provinces.province_id = patients.province_id;
```

8. Show how many patients have a birth_date with 2010 as the birth year. 
``` sql
SELECT COUNT() AS patient_2010
FROM patients
WHERE YEAR(birth_date)=2010;
```

9. Show the first_name, last_name, and height of the patient with the greatest height.
``` sql
SELECT first_name, last_name, MAX(height) AS height
FROM patients;
```

10. Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000
``` sql
SELECT * FROM patients
WHERE patient_id IN (1,45,534,879,1000);
```

11. Show the total number of admissions
``` sql
SELECT COUNT(*) AS total_admission 
FROM admissions;
```

12. Show all the columns from admissions where the patient was admitted and discharged on the same day.
``` sql
SELECT *
FROM admissions
WHERE admission_date=discharge_date;
```

13. Show the total number of admissions for patient_id 573.
``` sql
SELECT patient_id, COUNT() AS admission_573
FROM admissions
WHERE patient_id=573;
```
