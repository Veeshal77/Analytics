# Analytics

This Power BI dashboard provides key insights into:
- Summary by gender: employee numbers, Avg annual salary, and bonus.
- Workforce demographics by country, ethnicity, and age group.
- Correlation between Annual Salary($) and Bonus%
- Salary distribution across business units, country and job levels 

Highlights: 
- Used Parameters / slicers to allow users to switch between dimensions
- Leveraged DAX functions to create custom measures
- Created Dumb bell chart using line charts to visualize min/max of annual salary

Steps:
- Load data from input excel file into power bi desktop. import datasets for Employees and job levels
- In the Table view, preview the data in both data sets.
- It was observed that the Job level datasets has column headers named Column1 and Column2 and the headers were showing as the first row. To set the correct headers, click on Transform Data -> Transform tab -> Use First Row as Headers -> Select Use First Row as Headers
- Merge "Job Level" column from Job levels dataset into the Employees dataset:
 Transform Data -> Home tab -> Merge Queries -> Select Employees.Job_title,Job_Level.Job_title and merge using left outer join

Go to Report View 
Under Data section do the following:
- Add measure Avg Annual Salary for Females = 
AVERAGEX(
	FILTER('TBL_Employees',Lower('TBL_Employees'[Gender])="female"),
	CALCULATE(SUM('TBL_Employees'[Annual Salary]))
)
- Add measure Avg Annual Salary for Males = 
AVERAGEX(
	FILTER('TBL_Employees',Lower('TBL_Employees'[Gender])="male"),
	CALCULATE(SUM('TBL_Employees'[Annual Salary]))
)
- Add measure Avg Bonus % for Females = 
AVERAGEX(
	Filter('TBL_Employees',Upper('TBL_Employees'[Gender])= "FEMALE"),
	CALCULATE(SUM('TBL_Employees'[Bonus %]))
)
- Add measure Avg Bonus % for Males = 
AVERAGEX(
	Filter('TBL_Employees',Upper('TBL_Employees'[Gender])= "MALE"),
	CALCULATE(SUM('TBL_Employees'[Bonus %]))
)
- Add measure Count of Females = Calculate(COUNTROWS('TBL_Employees'),lower('TBL_Employees'[Gender])="female")
- Add measure Count of Males = Calculate(COUNTROWS('TBL_Employees'),lower('TBL_Employees'[Gender])="male")

Under Visualizations:
- Add Text box = "SUMMARY" 
- Select Card -> Add data to visual -> Fields="Count of Females" -> Format your visual -> Visual -> Callout Value -> Font Style=Verdana,Size = 15,Color=Pink -> Category Label -> Font = Verdana, size=12 -> General -> Data Format -> Apply setting to="Employee Count"
- Select Card -> Add data to visual -> Fields="Avg Annual Salary for Females" -> Format your visual -> Visual -> Callout Value ->Font Style=Verdana,Size = 15,Color=Pink -> Category Label -> Font = Verdana, size=12 -> General ->Data Format -> Apply setting to="Avg Annual Salary" -> Format Options -> Format="Currency" -> Currency Format="$"
- Select Card -> Add data to visual -> Fields="Avg Bonus % for Females" -> Format your visual -> Visual -> Callout Value ->Font Style=Verdana,Size = 15,Color=Pink -> Category Label -> Font = Verdana, size=12 -> General ->Data Format -> Apply setting to="Avg Bonus" -> Format Options -> Format="Percentage" ->
- Similarly, add 3 cards for Males employee count, Average Annual Salary and Avg Bonus%

-Under Visualizations:
Demography Section:
- Select Donut chart -> Add data to your visual -> legend="Country" -> Values="Count of Country" -> Visual -> Slices -> set Colors -> Spacing -> Inner radius="80%" -> Details label -> Option ->Position="Prefer outside" -> label contents = "Category, percent of total"
- Similarly, add donut chart for Ethnicity
- To create Age Group donut, first create Age groups based on the Age data in Employees table
- Table View -> Add Column -> Age Group = SWITCH(True(),'TBL_Employees'[Age] < 25, "Under 25 Years",
				'TBL_Employees'[Age] >= 25 && 'TBL_Employees'[Age] < 45, "25 - 44 Years",
				'TBL_Employees'[Age] >= 45 && 'TBL_Employees'[Age] < 65, "45 - 64 Years",
				"65 Years or older")
- Report View -> Add donut chart for Age group following previous steps from Country or Ethnicity donut charts 

Annual Salary and Bonus %
-Under Visualizations:
- Select Scatter chart -> Add data to your visual -> X axis="Annual Salary" -> Y axis="Bonus %" -> Visual -> X axis -> Type = "Continuous" -> Range -> Minimum=10000, Maximum=300000 -> Values -> Display unit="Thousands" -> Title="On" -> Y axis -> Values="On" -> Title="On" -> Gridlines -> Horizontal="Off", Vertical="Off" -> General -> Padding = "0px" -> Title ="On"

Annual Salary Distribution
- Create  parameter field to allow users to switch between dimensions:
- Go to Modelling -> New Parameter -> Fields -> Name = dCategory -> Add and reorder fields="Business unit, Country, Job level -> Select "Add slicer to page" -> Create
- Create column -> Annual Salary 2 = Annual Salary 2 = TBL_Employees[Annual Salary]
- Under Visualizations:
- Select Line Chart -> X-axis="dCategory", Y-axis="Max of Annual Salary", "Min of Annual Salary2" -> Visual -> Values="On" -> Title="Off" -> Layout -> Maximum category width = "50px" -> Y-axis -> Range -> Min=0, Max=300000 -> Values="On" -> Title="Off" -> Markers="On" -> Add further Analysis to Visual -> Error Bars -> Apply Settings to -> series="Max of Annual Salary" -> Options -> Enabled="On" -> Upper bound="Max of Annual salary" -> Lower bound="Min of Annual Salary" -> Bar="On" -> Markers="Off" -> Tooltip="On"  

- HR Data Analysis dashboard:
  ![Dashboard](https://github.com/user-attachments/assets/2871da70-ddcc-4efc-aae0-80f1c4d2257b)
