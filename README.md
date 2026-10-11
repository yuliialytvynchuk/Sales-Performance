# Sales Performance Dashboard | Power BI

## Project Overview

This project explores sales performance using an interactive Power BI dashboard. The goal is to help stakeholders understand sales trends, evaluate product performance, compare business performance across different periods, and explore sales across customer locations.
The dashboard analyses sales, profit, quantity sold, discounts, and net sales. Interactive filters and visualisations allow users to explore the data from different perspectives.

## Business Questions:

1. Which five products perform best and worst in terms of sales, profit, and quantity sold?
2. How do sales trends change over time (daily, monthly, quarterly, and annually)?
3. What is the relationship between net sales and profit?
4. How do sales, profit, and quantity sold compare between two selected periods?
5. What is the average discount across different product categories?
6. How many transaction records are included in the dataset?
7. How can users filter and explore detailed sales information by date, customer, product, and promotion?
8. How does sales performance vary across cities?

## Steps followed:

### Data ptofiling and Transformation

- Step 1: Loaded the dataset, provided as an Excel (.xlsx) file, into Power BI Desktop.
- Step 2: Opened Power Query Editor and, under the View tab in the Data Preview section, enabled Column Distribution, Column Quality, and Column Profile for all four tables in the dataset to examine the quality and distribution of the data.
- Step 3: By default, column profiling is based on the first 1,000 rows. To analyse the complete dataset, selected Column profiling based on entire dataset for each table.
- Step 4: In the Price Reduction Type column, descriptions of discounts were provided instead of numerical percentages. To address this, created a conditional column named Percentage to represent each discount as a percentage.
- Step 5: In the Fact Table, changed the data types of the CustomerID and PromotionID columns to text because these columns contain identifiers rather than values intended for numerical calculations.
- Step 6: Several columns in the Fact Table contained 100% empty values. To populate Price per Unit, performed a left outer join with the Dim Product table, which contained the required information. Used Product ID as the matching column, expanded the resulting column, and renamed it to Price per Unit. Removed the original empty column.
- Step 7: The Total Sales column also contained 100% empty values. Created a custom column named Total Sales New by multiplying Units Sold by Price per Unit. Changed its data type to a whole number and removed the original empty column.
- Step 8: The Discount Percentage column in the Fact Table was 100% empty. Performed a left outer join with the Dim Promotion table to retrieve the discount percentages. Replaced null values with 0, representing transactions with no recorded discount, and removed the original empty column.
- Step 9: The Discount Value column was also empty. Created a custom column named Discount Value New by multiplying Total Sales New by Discount Percentage and dividing the result by 100. Changed the data type to decimal and removed the original empty column.
- Step 10: The Net Sales column was empty. Created a custom column by subtracting Discount Value New from Total Sales New and removed the original empty column.
- Step 11: Established a star schema in the Data Model view by creating one-to-many relationships from Dim Product, Dim Customers, and Dim Promotion to the Fact Table.

The dataset was now prepared for visualisation and further analysis.

### Visualisation

#### Question 1: Which are the top and bottom five products by sales, profit, and quantity sold?

- Step 12: Created bar charts to display the top and bottom five products. Applied Top N and Bottom N filters to identify the products with the highest and lowest values for the selected metrics.

<img width="602" height="325" alt="Top-Bottom 5" src="https://github.com/user-attachments/assets/944acebc-1ab3-4dde-95a6-cb2654b07937" />

Insights: The charts highlight differences in product performance across sales, profit, and quantity sold. Products that perform well can be identified alongside those with weaker results. This information can support decisions about product range, inventory management, and future sales strategies. However, low sales or profit alone may not be sufficient reason to discontinue a product; costs, demand, and strategic importance should also be considered.


#### Question 2: How do sales trends vary over time (daily, monthly, querterly, annually)?

- Step 13: Created a line chart using the Date and Net Sales New columns to visualise changes in net sales over time.
- Step 14: Used the drill-up function to view sales at the yearly level. Moving down the date hierarchy allowed the visualisation to display quarterly, monthly, and daily sales.
- Step 15: Used the drill-down function to investigate sales within a particular year, quarter, month, or day.

<img width="560" height="301" alt="Years" src="https://github.com/user-attachments/assets/8d19f1dc-df56-4d3b-aeb8-c096927a39d1" />
<img width="560" height="298" alt="Year 2023 Drill down" src="https://github.com/user-attachments/assets/23f03199-910c-472b-b47a-ea5e9a5a228e" />

Insights: The visualisation indicates that the second quarter has the lowest sales and the fourth quarter has the highest sales in each year shown. The increase in Q4 could be associated with seasonal demand and Christmas shopping. However, this is a possible explanation rather than a confirmed cause. Further analysis of monthly sales and product categories could help determine which periods and products contribute most to this pattern.


#### Question 3: What is the relationship between sales and profit?

- Step 16: Created a scatter plot using Profit and Net Sales New, with both fields set to Don't summarise so that individual records could be examined.

<img width="575" height="310" alt="Profit vs Sales" src="https://github.com/user-attachments/assets/8b9cc245-a96e-4a51-90f4-15045c31271c" />

Insights: The scatter plot suggests a positive relationship between net sales and profit: transactions with higher sales values generally tend to have higher profits. However, the points are more dispersed at higher values, and there are fewer observations in the higher-sales range. This may indicate that high-value transactions are less common. Further analysis would be needed to determine how factors such as discounts, product type, and costs influence profit margins.


#### Question 4: How can sales, profit, and quantity sold be compared between any two periods selected by the user?

- Step 17: Created two date slicers using the Date column, allowing the user to select two separate periods.
- Step 18: Created two sets of three bar charts to display Net Sales New, Profit, and Units Sold for each selected period.
- Step 19: Used Edit interactions to disable the first date slicer's interaction with the three charts intended for the second period.
- Step 20: Applied the same approach to the second date slicer, disabling its interaction with the three charts intended for the first period.
- Step 21: Configured the interactions so that each date slicer controls only its corresponding set of three charts. This allows the two periods to be compared independently.

<img width="601" height="319" alt="Two slicers" src="https://github.com/user-attachments/assets/c0559d79-168e-476b-b15a-ec1c5a5e1990" />

Insights: This interactive view enables stakeholders to compare two selected periods side by side. They can examine changes in net sales, profit, and units sold simultaneously, helping identify whether changes in revenue are accompanied by changes in sales volume and profitability. This can be useful for evaluating seasonal performance or comparing results before and after a particular business event.


#### Question 5: What is the average discount offered for each promotion?

- Step 22: Created a bar chart using the average discount percentage and Promotion Name to compare the discount levels associated with different promotions.

<img width="575" height="235" alt="Discount" src="https://github.com/user-attachments/assets/5c8905ec-f1f5-42f3-9ed3-d228198092dd" />

Insights: The visualisation allows the user to identify promotions associated with the highest and lowest average discount percentages. This can support the evaluation of discount strategies.


#### Question 6: What is total number of orders?

- Step 23: Added an index column to the Fact Table, starting from 1, and renamed it Order ID. Changed its data type to text so that it would be treated as an identifier.
- Step 24: Created a card visual using Order ID and configured the aggregation to count distinct values, displaying the number of unique order IDs in the dataset.

<img width="64" height="47" alt="Orders" src="https://github.com/user-attachments/assets/c83ce956-bf53-4803-bdab-1b7299357472" />

Insights: The card provides a quick overview of the number of distinct IDs assigned to the records in the dataset. This metric can help stakeholders understand the scale of the data being analysed.


#### Question 7: How can sales, profit, discounts, net sales, and other order-level fields be explored using filters?

- Step 25: Created a table visual containing the relevant columns from the Fact Table. Configured the fields not to be summarised so that the table could display record-level information.
- Step 26: Added four slicers to the report using Date, Customer Name, Product Name, and Promotion Name to filter the table.
- Step 27: Since the slicers use fields from dimension tables and the filtering behaviour required additional configuration, created a measure named Sum Dim:
```sql
Sum Dim = SUM('Fact Table'[Net Sales New])
```
Added this measure to the visual-level filters for the relevant slicers, configuring the filter to exclude blank values.

<img width="600" height="337" alt="Slicer 1" src="https://github.com/user-attachments/assets/d4bc50d8-3074-44ee-b878-288735673973" />
<img width="593" height="328" alt="Slicer2" src="https://github.com/user-attachments/assets/1de42a22-ab02-475b-9533-c88b0d21eb30" />

Insights: The additional filtering configuration allows the slicers to work together more effectively. When one slicer is used, the others can display the relevant available values, making it easier to narrow down the data by date, customer, product, or promotion. The table provides a more detailed view of individual records and can help stakeholders investigate specific transactions without manually searching through the entire dataset.


#### Question 8: How do sales vary across different cities?

- Step 28: Created a map visual using the City column from the Dim Customers table. Set the data category of City to City to help Power BI interpret the geographic information correctly. Used the sum of Net Sales New to determine the bubble size, allowing sales values to be compared across cities.

<img width="538" height="288" alt="City" src="https://github.com/user-attachments/assets/51396b5d-2d34-4b12-aa50-dbef62a768fa" />

Insights: The map provides a geographical overview of sales performance and helps identify cities that contribute the most and least to total net sales. This information could support decisions about regional marketing and future sales opportunities.
