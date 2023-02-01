> # Attrition in an Organization || Exploring the possible Factors?
> 

 

*Data Source* : IBM HR ANALYTICS DATA,
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





![pic](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/Screen%20Shot%202023-01-29%20at%2010.51.24%20PM.png)



##  2.3 ERD
> Creating Entity Relationship Diagram

![ERD](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/ERD_HR.png)

# STEP 3

## Exploratory Data Analysis
 

 Number of rows in data - Checking Number of Rows in the dataset

``` SQL
SELECT count(*) FROM HR_DB.Employees;
```

 Number of unique id's in the dataset
``` SQL
Select count(DISTINCT EmployeeNumber) FROM HR_DB.Employees; 
```
 #### Summary:
 - Number of Total Observation : ==1470== 
 - Employee Number is the ==unique id column==

> **Employee Analysis**
> 
*Average Age of Employees:* **37 Years**
``` sql
SELECT AVG(AGE) as Average_Age
FROM HR_DB.Employees;
```
*Average Salary of Employees:* **6502**

``` sql
SELECT AVG(Sal_Monthly_Income) as Average_Salary
FROM HR_DB.Employees;
```
*Male Female Ratio:*  **40% Female 60% Male**

``` sql
SELECT GENDER, COUNT(*) as Frequency, Round(Count(*)/sum(count(*)) over (),2) as Percentage
FROM HR_DB.Employees
GROUP BY Gender;
```




> **Attrition Analysis**

*Overall Employee Attrition:*

``` sql
SELECT Attrition, count(*) as Frequency, Round(100* count(*)/sum(count(*)) over(),2) as Percentage
FROM HR_DB.Employees
GROUP BY Attrition;
```

![Attrition](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/Attrition.png)

*Attrition by Gender:*
``` sql
SELECT Gender , Attrition , Count(*) as Frequency , Round(Count(*)/sum(count(*)) over (partition by Gender),2) as Percentage
FROM HR_DB.Employees 
GROUP BY Gender, Attrition;
```
*Department wise Attrition:*

```sql
SELECT Dept_Name,count(*) as Attrition_Frequency, Round(100*count(*)/sum(count(*)) over (),2) as Percentage
FROM HR_DB.Employees as a
INNER JOIN HR_DB.Department as b
on a.Dept_ID = b.Dept_ID
WHERE Attrition = 'Yes'
GROUP BY Dept_Name
ORDER BY Attrition_Frequency DESC;
```
![PIC](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/DEPT_ATTRITION.png)

#### Summary:
- Attrition Count: ==237==
 - Employee Attrition Rate : ==16%==
 - Attrition Rate by Gender: Male (==17%== Attrition Rate), Female (==15%== Attrition Rate)
 - Highest Attrition is seen in R&D Department (56%) followed by sales department (39%) and lowest in HR Department (5%)

> **Impact of Salary on Attrition**

*Income is generally considered one of the main reason for Employee Attrition in a company*
*In this section we will analyze the impact of salary on Attrition and find answers for the following business questions:*

1. What is the effect of salary on Attrition? Are there any significant differences between salary of individuals who quit and didn't quit?
3.  Is job satisfaction related to salary? What is its effect on Attrition
4. Average salary difference between department
5. Avg salary of people who left the organization, job satisfaction for those people, salary hike they recieved.
6. Attrition by Job role and salary difference

*Average salary difference between departments:*

``` sql
SELECT Dept_Name, Avg(Sal_Monthly_Income) as Avg_sal
FROM HR_DB.Employees as a
INNER JOIN HR_DB.Department as b
ON a.Dept_ID = b.Dept_ID
GROUP BY Dept_Name
ORDER BY Avg_Sal DESC;
```
![pix](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/Dept_slary.png)


*Avg_salary difference between people who quit the company and who didn't:*

``` sql
SELECT Attrition , Avg(sal_Monthly_Income) as Avg_sal
FROM HR_DB.Employees 
GROUP BY Attrition;
```
![pic](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/Salary_Attrition.png)

*Job Satisfaction, Avg_salary and Attrition*
``` sql
SELECT  b.jobsatfac_Type ,Attrition, Avg(Sal_Monthly_Income) as Avg_sal
FROM HR_DB.Employees as a
INNER JOIN HR_DB.Job_Satisfaction as b
on a.Jobsatisfaction = b.Jobsatisfaction
Group by 1,2
ORDER BY 1,2;
```
![pic](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/Jobsat_Attrition_sla.png)

*Attrition and salary hike*

``` sql
SELECT Attrition, Avg(PercentSalaryHike) as Avg_Sal_Hike
FROM HR_DB.Employees
GROUP BY 1; 
```
* Attrition by Job_Role

``` sql
SELECT Dept_Name , Name, Count(*) as Frequency  
FROM HR_DB.Employees as a
INNER JOIN HR_DB.Job_Role as b
ON a.JobRole_ID = b.JobRole_ID
INNER JOIN HR_DB.Department as c
on a.Dept_ID = c.Dept_ID
WHERE Attrition = 'yes'
Group by 1,2
ORDER BY Dep DESC;
;
```
![pic](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/Attrition_by_jobrole.png)

*Salary by job Role*

``` SQL
SELECT Dept_Name , Name, Avg(Sal_Monthly_Income) as Avg_sal 
FROM HR_DB.Employees as a
INNER JOIN HR_DB.Job_Role as b
ON a.JobRole_ID = b.JobRole_ID
INNER JOIN HR_DB.Department as c
on a.Dept_ID = c.Dept_ID
Group by 1,2
ORDER BY Avg_sal;
```
![PIC](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/SALARYBYJOBROLE.png)

*Overtime by Job Role*

``` sql
SELECT  Dept_Name, Name , count(*) as frequency
FROM HR_DB.Employees as a
INNER JOIN HR_DB.Job_Role as b
ON a.JobRole_ID = b.JobRole_ID
INNER JOIN HR_DB.Department as c
on a.Dept_ID = c.Dept_ID
WHERE Overtime = 'yes'
Group by 1,2
ORDER BY frequency DESC;
```

![pic](https://github.com/Shris2982/HR_DATA_ANALYTICS_SQL/blob/main/HR_ANALYTICS_PICS%22/Overtimebyjobrole.png)

#### Summary:

 - There is a ==huge difference in Avg. salary between people who did not quit (Higher) and people who quit (lower).== This suggest that salary has some factor to play in Attrition
 - Digging Deeper and further to this , we analyzed salary by job role and Attrition by job role 
 - There are ==4 major Job Role from which there is maximum Attrition.== Those are Laboratory Technician, Sales Executive, Research Scientist & Sales Representative
 -  Looking at the Avg.Salary for the job role , we can see 3 out of those 4 above ==(Sales Representative,Laboratory Technician,Research Scientist) are the job roles with the lowest salary range.== (Much lower than the average salary of6502). The minimum salary wage is a factor for Attrition in these job roles.
 - We looked further into another factor **"OVERTIME"** on Attrition in this job roles. We see that these are also the job roles where ==majority of people are doing overtime.== Sales executive who had salary range has one of the highest number of employee doing overtime. This can explain the high attrition rate in this Job roles.

































