# Hospital_Data_Analysis 


<p align="center">
  <img src="logo.png" width="200" alt="Project Logo">
</p>

## 🎯 Objectives

Practice SQL queries with real-world datasets.

Learn SQL concepts like aggregation, grouping, and date functions.

Solve business-related SQL problems for data analysis.

Improve query optimization and performance.

## 🏥 Dataset: Hospital Data

📂 Dataset Features:

🏥 Hospital Name

📍 Location

🏨 Departments

👨‍⚕️ Number of Doctors

👩‍⚕️ Number of Patients

🏥 Admission & Discharge Dates

💰 Medical Expenses

----

 ## 📝 Queries Included

📌 Key SQL Queries Covered:

📊 Total Patients Count in each hospital

🏥 Top 3 Hospital Departments with the highest patient count

💸 Hospital with the Highest Medical Expenses

📅 Average Stay Duration per Department

📆 Monthly Medical Expenses Analysis

🛏️ Longest Patient Stay Calculation

🌍 Total Patients per City

----
## 🏛 Database Schema
```sql
    CREATE TABLE Hospital_Data (
    hospital_name VARCHAR(255),
    location VARCHAR(100),
    department VARCHAR(100),
    doctors_count INT,
    patients_count INT,
    admission_date DATE,
    discharge_date DATE,
    medical_expenses DECIMAL(10,2)
);
```
---------------------------------
## Business Problems And Aanlysis:
-----------------------------------
1. Write an SQL query to find the total number of patients across all hospitals.
```sql
SELECT hospital_name,
       SUM(patients_count) AS total_patients 
FROM Hospital_Data
GROUP BY hospital_name;
```
----
2. Retrieve the average count of doctors available in each hospital.
```sql
SELECT hospital_name,
       AVG(doctors_count) AS average_doctors
FROM Hospital_Data
GROUP BY hospital_name;
```
-----

3. Find the top 3 hospital departments that have the highest number of patients.
```sql
SELECT department,
       patients_count 
FROM hospital_data
ORDER BY patients_count DESC
LIMIT 3;
```
----
4. Identify the hospital that recorded the highest medical expenses.
```sql
SELECT hospital_name,
       medical_expenses
FROM hospital_data
ORDER BY medical_expenses DESC
LIMIT 1;
```
----

5. Calculate the average medical expenses per day for each hospital
```sql
SELECT hospital_name, 
       AVG(medical_expenses / (COALESCE(NULLIF(discharge_date - admission_date, 0), 1))) AS avg_expenses_per_day
FROM Hospital_Data
GROUP BY hospital_name;
```
----

6. Find the patient with the longest stay by calculating the difference between Discharge Date and Admission Date.
```sql
SELECT hospital_name,
       patients_count ,
       (discharge_date - admission_date) AS Longest_stay
FROM hospital_data
ORDER BY Longest_stay DESC
LIMIT 1;
```
----

7.Count the total number of patients treated in each city.
```sql
SELECT  location,
        SUM(patients_count)AS total_patients
FROM hospital_data
GROUP BY location;
```
----

8.Calculate the average number of days patients spend in each department.
```sql
SELECT department,
       AVG(discharge_date - admission_date)AS Avg_spend_Days
FROM hospital_data
GROUP BY department;
```
----

9.Find the department with the least number of patients.
```sql
SELECT department,patients_count
FROM hospital_data
GROUP BY department,patients_count
ORDER BY patients_count ASC
LIMIT 1;
```

-----

10.Group the data by month and calculate the total medical expenses for each month.
```sql
SELECT 
    DATE_TRUNC('month', admission_date) AS month,
    SUM(medical_expenses) AS total_medical_expenses
FROM Hospital_Data
GROUP BY month
ORDER BY month;
```



