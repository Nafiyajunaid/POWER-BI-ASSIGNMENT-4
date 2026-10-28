# POWER-BI-ASSIGNMENT-4
Calculated Columns:
● Create a Calculated Column for 'Category Type': Add a calculated column in the Order Details table that combines the 'Category' and 'Sub-Category' columns into a single 'Category Type' column.
new column > category type = 'Order Details (1)'[Category]&" "&'Order Details (1)'[Sub-Category]

● Calculate Revenue per Order in Order Details Table: Create a calculated column in the Order Details table to compute the revenue (Amount * Quantity) per order.
new column > revenue per order = 'Order Details (1)'[Amount]*'Order Details (1)'[Quantity]

● Create a Calculated Column to Categorize Sales: Add a calculated column named ‘Sales Category’ in the Order Details table that categorizes each order as 'Above Average' or 'Below Average' based on the Amount value
new column > sales category = IF('Order Details (1)'[Amount]>AVERAGE('Order Details (1)'[Amount]),"above average","below average")

Calculated Measures:
● Calculate Order Count: Define a measure to count the total number of orders in the Order Details table.
new measure > total no of orders = DISTINCTCOUNT('List of Orders (1)'[Order ID])

● Calculate Average Profit in Delhi: Create a measure to calculate the average profit for orders placed in Delhi.
new measure > average profit in delhi = CALCULATE(AVERAGE('Order Details (1)'[Profit]),'List of Orders (1)'[City]="delhi")

● Calculate Year-to-Date (YTD) Sales: Define a measure to calculate the total sales amount accumulated from the earliest order date up to each order date.
new measure > min date = MIN('List of Orders (1)'[Order Date])
new measure > max date = MAX('List of Orders (1)'[Order Date])
new table > Date_table = ADDCOLUMNS(CALENDAR(DATE(2018,04,01),DATE(2019,03,31)),"Year", YEAR([Date]), "MonthNumber",MONTH([Date]),"Month_name",FORMAT([Date],"MMMM"),"Quarter", "Q" & QUARTER([Date]), "Day", DAY([Date]), "Dayname", FORMAT([Date],"DDDD"))
new measure > YTD Sales = TOTALYTD(SUM('Order Details (1)'[Amount]),Date_table[Date])


Data Visualization:
Sales Target Achievement by Category: Compare actual sales with sales targets by category using a clustered column chart.
select clustered column chart .X-axis:Category Y-axis:amount Y-axis:Target

Max Profit Margin by Sub-Category: Analyze the maximum profit margin for each sub-category of products using a donut chart.
new column > profit margin = ('Order Details (1)'[Profit]/'Order Details (1)'[Amount])*100
Select Donut Chart. Legend: Sub-Category, Values: Profit Margin (Maximum)

Monthly Sales Trend: Show the trend of monthly sales over time using a line chart.
Select Line Chart. X-axis: Month name, Y-axis: Sum of Amount.

Comparison of Profit and Quantity by Sub-Category: Compare the relationship between profit and quantity sold for different sub-categories using a scatter chart.
Select Scatter Chart. X-axis: Sum of Quantity, Y-axis: Sum of Profit, Legend: Sub-Category.

Comparison of Total Sales Amount and Target: Create cards to succinctly display the total sales amount alongside the sales target for quick comparison and analysis. Also, create a multi-row card to display the minimum target for each segment.
Select Card. Fields: Sum of Amount. Create another Card with Sum of Target.
Select Multi-Row Card. Fields: Category, Minimum of Target.


Sales Performance Matrix: Build a matrix view to analyze how actual sales compare to sales targets across different categories and months.
Select Matrix. Rows:Month name , Columns: Category, Values: Sum of Amount, Sum of Target.

Geographic Sales Analysis: Visualize total sales on a map by city to identify regional sales patterns.
Select Map. Location: City, Bubble Size: Sum of Amount.

Sales Distribution by Sub-Category: Represent the sales distribution across different sub-categories using a treemap.
Select Treemap. Group: Sub-Category, Values: Sum of Amount.

Order Count Analysis by State: Create a funnel chart to visualize the distribution of order counts across different states
Select Funnel Chart. Category: State, Values: total no of orders.
