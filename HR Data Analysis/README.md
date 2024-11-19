# Analytics

This Power BI dashboard provides key insights into:
- Summary by gender: employee numbers, Avg annual salary, and bonus.
- Workforce demographics by country, ethnicity, and age group.
- Correlation between Annual Salary($) and Bonus%
- Salary distribution across business units, country and job levels 

Highlights: 
- Used Parameters / slicers to allow users to switch between dimensions
- Createed custom measures using DAX functions 
- Generated a Dumb bell chart using line charts to visualize min/max of annual salary

Steps:
- Load data from input excel file into power bi desktop. import datasets for Employees and job levels
- In the Table view, preview the data in both data sets.
- It was observed that the Job level datasets has column headers named Column1 and Column2 and the headers were showing as the first row. To set the correct headers, click on Transform Data -> Transform tab -> Use First Row as Headers -> Select Use First Row as Headers
- Merge "Job Level" column from Job levels dataset into the Employees dataset:
 Transform Data -> Home tab -> Merge Queries -> Select Employees.Job_title,Job_Level.Job_title and merge using left outer join

Under Data section add the following measures:
- Avg Annual Salary for Females = 
AVERAGEX(
	FILTER('TBL_Employees',Lower('TBL_Employees'[Gender])="female"),
	CALCULATE(SUM('TBL_Employees'[Annual Salary]))
)
- Avg Annual Salary for Males = 
AVERAGEX(
	FILTER('TBL_Employees',Lower('TBL_Employees'[Gender])="male"),
	CALCULATE(SUM('TBL_Employees'[Annual Salary]))
)
- Avg Bonus % for Females = 
AVERAGEX(
	Filter('TBL_Employees',Upper('TBL_Employees'[Gender])= "FEMALE"),
	CALCULATE(SUM('TBL_Employees'[Bonus %]))
)
- Avg Bonus % for Males = 
AVERAGEX(
	Filter('TBL_Employees',Upper('TBL_Employees'[Gender])= "MALE"),
	CALCULATE(SUM('TBL_Employees'[Bonus %]))
)
- Count of Females = Calculate(COUNTROWS('TBL_Employees'),lower('TBL_Employees'[Gender])="female")
- Count of Males = Calculate(COUNTROWS('TBL_Employees'),lower('TBL_Employees'[Gender])="male")

- Create a date table using Power Query or DAX
- 
Under Visualizations:
- Add Summary section and underneadth add cards for Employee count, Avg. Annual Salary and Avg Bonus% for both Female employees
- Similarly, add 3 cards for Males employee count, Average Annual Salary and Avg Bonus%
- Add Donut charts for Country, Ethnicity and Age Group
- Add Scatter plot to show distribution based on Annual Salary and Bonus %
- Annual Salary Distribution:
- Create  parameter field to allow users to switch between dimensions:
- Show salary distribution by Business Unit, Country and Job Level
- Plot count of employee hires by year and count of employee exits by year using the date table. 

- HR Data Analysis report:
  ![Dashboard](https://github.com/user-attachments/assets/2871da70-ddcc-4efc-aae0-80f1c4d2257b)

  ![Screenshot 2024-11-19 122724](https://github.com/user-attachments/assets/853ba75a-5d9b-4912-acea-0a47cfc5c4a5)
