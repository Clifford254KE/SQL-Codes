# SQL-Codes
---
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

The output looks shaggy in the birth_date and hire_date columns. I only need years- this is achieved by using extract query 
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
---
Other useful codes for the same dataset

```sql
This extracts birth_date and birth_month in different columns.
SELECT birth_date,
       EXTRACT(YEAR FROM birth_date) AS birth_year,
       EXTRACT(MONTH FROM birth_date) AS birth_month,
       EXTRACT(DAY FROM birth_date) AS birth_day
FROM employees.employees
ORDER BY birth_date DESC
LIMIT 100000;

This one adds the layer of age of employees when they were hired. This is obtained by hired year - birth year.
SELECT first_name,
       last_name,
       gender,
       EXTRACT(YEAR FROM birth_date) AS birth_year,
       EXTRACT(YEAR FROM hire_date) AS hired_year,
	   (EXTRACT(YEAR FROM hire_date) - EXTRACT(YEAR FROM birth_date)) AS age_when_hired
FROM employees.employees
WHERE gender = 'M'
LIMIT 100000;

```

Exploring different datasets using cross-join and round functions. There are two tables joined together to produce the required outcome. Therefore, the code below shows some adjustments made on the queries to achieve different results. *Production* is the name of the schema. Download *datalab_export_2024-05-28 02_11_34.csv* and *datalab_export_2024-05-28 02_12_03.csv* above
```sql
SELECT TOP 10000 * 
FROM production.stocks
CROSS JOIN production.products;

SELECT product_name,
	   model_year,
	   quantity AS quantity_produced,
	   list_price AS price_of_product
FROM  production.stocks
CROSS JOIN production.products;

SELECT TOP 1000 product_name,
	   model_year,
	   quantity AS quantity_produced,
	   ROUND(list_price, -1) AS price_of_product
FROM  production.stocks
CROSS JOIN production.products;

SELECT TOP 1000 product_name,
	   model_year,
	   quantity AS quantity_produced,
	   ROUND(list_price, 2) AS price_of_product
FROM  production.stocks
CROSS JOIN production.products;
```

OUTPUT

![OUTPUT](https://github.com/Clifford254KE/SQL-Codes/assets/140185917/be273272-da80-4e3a-87a1-f3b7e3115402)


