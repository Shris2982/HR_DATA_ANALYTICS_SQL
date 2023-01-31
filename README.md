# HR_DATA_ANALYTICS_SQL

> # Attrition in an Organization || Exploring the possible Factors?
> 

 

*Data Source* : IBM HR ANALYTICS DATA
*Tools Used* : MySQL

# STEP 1


> Data Exploration - Exploring the available data set provided in excel for the following objective:
> 

 1.  **Columns and Observations:** How many columns and observations is there in  dataset?
2. **Missing data:** Looking for missing data in our dataset?
3. **Data Type:** The different datatypes we are dealing with.
4. **Meaning of Data:** What is data trying to give insight about? What are the important columns that can give insights?
Which columns are redundant and non contributing and can be dropped for further analysis?
Which data is categorical type?
What is the output or insight we are trying to get from the data?

# STEP 2

> Relational Data Model - Exploring Data Entities and Relationship. Creating Entity Relationship Diagram

 1. **Creating a new schema for the HR Analytics data:**


`Drop Schema if exists HR_DB;` -- *Drops the existing schema if any*
`Create Schema HR_DB;`
`USE HR_DB;`

  2. **Creating Tables and Importing the data**
  
```SQL
Create table  HR_DB.Department
(Dept_ID INTEGER, 
Dept_Name VARCHAR(50),
    PRIMARY KEY (Dept_ID)
);

Create table  HR_DB.Education_Field
(Field_Id INTEGER,
EducationField_Name VARCHAR(50),
 Primary Key (Field_Id)
);

Create table  HR_DB.Education_level
(Level_Id	INTEGER,
Name VARCHAR(50),
Primary Key(Level_Id)
);

Create table  HR_DB.Travel
(Travel_ID	INTEGER,
Business_Travel VARCHAR(50),
Primary Key (Travel_ID)
);

Create table  HR_DB.Enviroment_satisfaction
(ESID INTEGER,
TYPES VARCHAR(20),
 PRIMARY KEY(ESID)
);

Create table  HR_DB.Job_Role
(JobRole_ID	INTEGER,
Name VARCHAR(50),
 PRIMARY KEY (JobRole_ID)
);

Create table  HR_DB.Job_Involvement
(JobInvolvement_Code	INTEGER,
Job_Involv_Type VARCHAR(20),
 PRIMARY KEY(JobInvolvement_Code)
);

ALTER TABLE HR_DB.Job_Involvement ADD JobLevel INTEGER;

Create table  HR_DB.Job_Satisfaction
(JobSatisfaction INTEGER,
Jobsatfac_Type VARCHAR(20),
 PRIMARY KEY(JobSatisfaction)
);

Create table  HR_DB.Relationship_satisfaction
(Rel_Sat_id INTEGER,
Rel_Sat_Type VARCHAR(20),
 PRIMARY KEY(Rel_Sat_id)
);

Create table  HR_DB.worklife_balance
(worklifebal_id INTEGER,
worklifebal_Type VARCHAR(20),
 PRIMARY KEY(worklifebal_id)
);

Create table  HR_DB.performance_rating
(PerfRating_id INTEGER,
PerfRating_Type VARCHAR(20),
 PRIMARY KEY(PerfRating_id)
);

Create table  HR_DB.Salary_Hike
(PercentSalaryHike INTEGER,
PerfRating_id INTEGER,
 PRIMARY KEY(PercentSalaryHike),
 CONSTRAINT PerfRating_id_FKEY FOREIGN KEY (PerfRating_id) REFERENCES HR_DB.performance_rating(PerfRating_id)
);


Create table  HR_DB.stock_option_level
(StockOptionLevel_id INTEGER,
StockOptionLevel_Type VARCHAR(20),
Primary Key (StockOptionLevel_id)
);

Create table  HR_DB.Employees
(EmployeeNumber INTEGER,
Age	INTEGER,
Attrition VARCHAR(50),
DistanceFromHome INTEGER,
Gender VARCHAR(50),
MaritalStatus VARCHAR(50),
Overtime VARCHAR(50),
NumCompaniesWorked	INTEGER,
YearsAtCompany	INTEGER,
Sal_Monthly_Income INTEGER,
PercentSalaryHike INTEGER,
YearsSinceLastPromotion INTEGER,
Dept_ID INTEGER,
Field_Id INTEGER,
Level_Id INTEGER,
Travel_ID INTEGER,
ESID INTEGER,
JobRole_ID INTEGER,
JobInvolvement_Code INTEGER,
JobSatisfaction  INTEGER,
Rel_Sat_id INTEGER,
StockOptionLevel_id INTEGER,
worklifebal_id INTEGER,
      PRIMARY KEY (EmployeeNumber),
	  CONSTRAINT PercentSalaryHike_FKEY FOREIGN KEY (PercentSalaryHike) REFERENCES HR_DB.Salary_Hike(PercentSalaryHike),
	  	  CONSTRAINT Dept_ID_FKEY FOREIGN KEY (Dept_ID) REFERENCES HR_DB.Department(Dept_ID),
	  CONSTRAINT Field_Id_FKEY FOREIGN KEY (Field_Id) REFERENCES HR_DB.Education_Field(Field_Id),
	  CONSTRAINT Level_Id_FKEY FOREIGN KEY (Level_Id) REFERENCES HR_DB.Education_level(Level_Id),
	  CONSTRAINT Travel_ID_FKEY FOREIGN KEY (Travel_ID) REFERENCES HR_DB.Travel(Travel_ID),
	  CONSTRAINT ESID_FKEY FOREIGN KEY (ESID) REFERENCES HR_DB.Enviroment_satisfaction(ESID),
	  CONSTRAINT JobRole_ID_FKEY FOREIGN KEY (JobRole_ID) REFERENCES HR_DB.Job_Role(JobRole_ID),
	  CONSTRAINT JobInvolvement_Code_FKEY FOREIGN KEY (JobInvolvement_Code) REFERENCES HR_DB.Job_Involvement(JobInvolvement_Code),
	  CONSTRAINT JobSatisfaction_FKEY FOREIGN KEY (JobSatisfaction) REFERENCES HR_DB.Job_Satisfaction(JobSatisfaction),
	  CONSTRAINT Rel_Sat_id_FKEY FOREIGN KEY (Rel_Sat_id) REFERENCES HR_DB.Relationship_satisfaction(Rel_Sat_id),
	  CONSTRAINT worklifebal_id_FKEY FOREIGN KEY (worklifebal_id) REFERENCES HR_DB.worklife_balance(worklifebal_id)
);
```

## 2.1 IMPORTING DATASET

The Dataset for all Tables were imported via utilizing the ***SQL SERVER IMPORT AND EXPORT WIZARD***

## 2.2 Analyzing Physical Database in the schema
 
``` SQL
SELECT * FROM HR_DB.Department limit 10;

SELECT * FROM HR_DB.Education_Field LIMIT 10;
SELECT * FROM HR_DB.Education_level LIMIT 10;
SELECT * FROM HR_DB.Enviroment_satisfaction LIMIT 10;
SELECT * FROM HR_DB.Job_Involvement;
SELECT * FROM HR_DB.Job_Role;
SELECT * FROM HR_DB.Job_Satisfaction;
SELECT * FROM HR_DB.performance_rating;
SELECT * FROM HR_DB.Relationship_satisfaction;
SELECT * FROM HR_DB.Salary_Hike;
SELECT * FROM HR_DB.Travel;
SELECT * FROM HR_DB.worklife_balance;
SELECT * FROM HR_DB.Employees LIMIT 10;
```





![pic](https://github.com/Shris2982/HR_DATA_ANALYTICS/blob/main/Screen%20Shot%202023-01-29%20at%2010.51.24%20PM.png)



##  2.3 ERD
> Creating Entity Relationship Diagram

![ERD](https://github.com/Shris2982/HR_DATA_ANALYTICS/blob/main/ERD_HR.png)

# STEP 3

## Exploratory Data Analysis
 

 - Number of rows in data - Checking Number of Rows in the dataset

``` SQL
SELECT count(*) FROM HR_DB.Employees;
```

- Number of unique id's in the dataset
``` SQL
Select count(DISTINCT EmployeeNumber) FROM HR_DB.Employees; 
```

## Attrition Analysis

``` sql
SELECT Attrition, count(*) as Frequency
FROM HR_DB.Employees
GROUP BY Attrition;
```


SELECT Gender, Maritalstatus, count(*) as frequency,
Round(100* count(*) /sum(count(*)) over(Partition by Gender),2) as percentage
FROM HR_DB.Employees
GROUP BY Gender, MaritalStatus
Order by Gender;
# Grouping. y Age
SELECT COUNT(DISTINCT Age) from HR_DB.Employees;
SELECT Age, Count(*) as freq
FROM HR_DB.EMPLOYEES
GROUP BY Age
ORDER BY freq DESC;
# Attrition by Gender
SELECT Attrition, Gender , count(*) as Frequency,
100 * count(*)/sum(count(*)) over (partition by Attrition) as percentage,
count(*)/sum(count(*)) over (partition by Gender) as churn_by_gender
FROM HR_DB.Employees
GROUP BY Attrition, Gender
ORDER BY Attrition DESC;

SELECT Gender, count(*) as Count_no, Round(100 * count(*)/sum(count(*)) over (),2) as percentage
FROM HR_DB.Employees
Group by Gender;

#Attrition by Department 

SELECT Dept_Name,count(*) as Attrition_Frequency
FROM HR_DB.Employees as a
INNER JOIN HR_DB.Department as b
on a.Dept_ID = b.Dept_ID
WHERE Attrition = 'Yes'
GROUP BY Dept_Name
ORDER BY Attrition_Frequency DESC;

#Attrition by overtime
SELECT Attrition, count(*) FROM HR_DB.Employees 
GROUP BY Attrition;
SELECT Count(Overtime) FROM HR_DB.Employees;
SELECT overtime , count(*)
FROM HR_DB.Employees
Where Attrition = 'Yes'
Group by Overtime;

#OVERTIME BY GENDER
SELECT Gender, Overtime, count(*) as frequency, 
 Round( 100 * count(*)/sum(count(*)) over(),2) as percentage
FROM HR_DB.Employees
Group by Gender, Overtime
Order by overtime DESC;
































