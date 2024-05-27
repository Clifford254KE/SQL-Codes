# SQL-Codes

### This repository displays different SQL codes to answer various questions using different datasets.


### QUESTION 1
Using the employees' dataset, extract first_name, last_name, gender, year of birth, year hired, and ranking (based on new employees- those hired in 1990 and above, junior employees- those hired in 1988-1990, and senior employees- hired in 1987 or earlier). Go ahead and  provide the list of junior employees in ascending order.

This is how the dataset looks like before answering the question.
```sql
SELECT *
FROM employees.employees;

```
OUTPUT

![SQL1](https://github.com/Clifford254KE/SQL-Codes/assets/140185917/b9a28bdf-4585-4b0a-921d-2b095e15fe97)

The output looks shaggy in the birth_date and hire_date columns. I only need years- this is achieved using extract query 
The code written below answers the question above. 
```sql
SELECT first_name,
       last_name,
       gender,
       EXTRACT(YEAR FROM birth_date) AS birth_year,
       EXTRACT(YEAR FROM hire_date) AS hired_year,
	   (EXTRACT(YEAR FROM hire_date) - EXTRACT(YEAR FROM birth_date)) AS age_when_hired,
	   (CASE WHEN (EXTRACT(YEAR FROM hire_date))>= '1990' THEN 'New_empoloyee'
			 WHEN (EXTRACT(YEAR FROM hire_date))>= '1988' THEN 'Junior_employees'
			ELSE 'sinior_employee' END) AS employee_ranking
FROM employees.employees
WHERE (EXTRACT(YEAR FROM hire_date))>= '1988' 
ORDER BY (EXTRACT(YEAR FROM hire_date) - EXTRACT(YEAR FROM birth_date));
```

OUTPUT

![SQL2](https://github.com/Clifford254KE/SQL-Codes/assets/140185917/38ddda01-ac75-435b-882e-e4ea6ab3b017)

NB. The original dataset (data A) and final output (data B) are uploaded above. 

