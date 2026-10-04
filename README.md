# Sales-Dashboard

## Problem Statement

This dashboard helps stakeholders understand their sales better. It helps the company know what their top/bottom 5 products are by sales, profit and quantity. It shows how sales trends vary overtime, relationships between sales and profit.
The dashboard also lets stakeholders compare sales, profit and quantity sold between two periods selected by them.
Additionally, it shows average dicounts offered in each category, and sales by different cities.
Sales, profit, discount, net sales and other remaining fields can also be filtered using visual filters to discover insights.

## Steps followed:

### Data ptofiling and Transformation

- Step 1 : Load data into Power BI Desktop, the dataset is a xlsx file.
- Step 2 : Open power query editor and in view tab under Data preview section, check "Column distribution", "Column quality" and "Column profile" options for 4 tables present in the Dataset.
- Step 3 : Also since by default, tables will be opened only for 1000 rows so you need to select "Column profiling based on entire dataset".
- Step 4: In the column "Price Reduction Type" description of the dicount was present instead of the percentages. For this purpose a new conditional "Percentage" columnn was added to represent a dicount in percentages.
- Step 5 : In the "Fact Table" the data type was changed to text for "CustomerID", "PromotionID" columns as you do not need it as numerical.
- Step 6. In the "Fact Table" several columns had 100% empty values. For the "Price per Unit" column a left join was performed with a "Dim Product" table that had "Price per Unit", using "Product ID" to connect them. A new column was renamed to "Price per Unit" and the old one was dropped.
- Step 7: "Total Sales" also had 100% empty values, so a new custom column "Total Sales New" was created by multiplying "Unit Sold" and "Price per Unit" columns. The data type was changed to whole numbers. Old column was dropped.
- Step 8: "Discount Percentage" column in "Fact Table" was 100% empty, so left join was performed with "Dim Promotion" table. Null values were replaced by 0 representing 0 discount. Old column was dropped.
- Step 9: "Dicount Value" column was also empty, so a new custom column "Discount Value New" was created where values from "Total Sales" column were multiplied by "Discount Percentage" and divided by 100. The data type was changed to decimal. Old column was dropped.
- Step 10: The column "Net Sales" was empty, so a new custom column was created where "Discount Value New" was deducted from "Total Sales". Old column was dropped.
- Step 11: Star Schema was performed in Data modelling where "One to many "relationships between tables were established from "Dim Product", "Dim Customers" and "Dim Promotion" to "Fact Table".


### Visualisation

Question 1: Top/Bottom 5 product by Sales/Profit/Quantity Sold.

- Step 12: Bar chart was used to represent top and bottom sales. Each bar chart was filtered by either top or bottom 5 N.

<img width="602" height="325" alt="Top-Bottom 5" src="https://github.com/user-attachments/assets/944acebc-1ab3-4dde-95a6-cb2654b07937" />

Question 2: How do sales trends vary over time (daily, monthly, querterly, annually)?

- Step 13: Line chart was used with "Net sales" and "Date" columns.
- Step 14: Drill up function on the visual was used to show the visualisation for years. Going to the next level in the hierarchy changed the visualisation to querters, months and days.
- Step 15: Drill down function enabled checking perticular year, month, or day.

<img width="560" height="301" alt="Years" src="https://github.com/user-attachments/assets/8d19f1dc-df56-4d3b-aeb8-c096927a39d1" />
<img width="560" height="298" alt="Year 2023 Drill down" src="https://github.com/user-attachments/assets/23f03199-910c-472b-b47a-ea5e9a5a228e" />


Question 3: Relationship between sales and profit.

- Step 16: Scatter plot with "Profit" and "Net Sales New" was created. No columns were summarised.There is linear relationship between Profit and Sales. The density though becomes smaller when numbers increase.

<img width="575" height="310" alt="Profit vs Sales" src="https://github.com/user-attachments/assets/8b9cc245-a96e-4a51-90f4-15045c31271c" />

Question 4: Compare sales/profit/quantity between any two periods selected by the user.

- Step 17: Two slicers were created with "Date" column.
- Step 18: Two seperate bar charts were created per each column ("Net Sales", "Profit", ""Units Sold").
- Step 19: The first slicer was formatted - edit interactions - and three bar charts were disabled to interact with it.
- Step 20: The same was performed for the second slicer.
- Step 21: Such edit enambles three bar charts to interact only with the first slicer when the date is changed, while other three bar charts only will interact when the date in the second slicer is changd.

<img width="601" height="319" alt="Two slicers" src="https://github.com/user-attachments/assets/c0559d79-168e-476b-b15a-ec1c5a5e1990" />


Question 5: Average discount offered in each category.

- Step 22: Bar chart wa used with average "Discount" and "Promotion Name".

<img width="575" height="235" alt="Discount" src="https://github.com/user-attachments/assets/5c8905ec-f1f5-42f3-9ed3-d228198092dd" />

Question 6: What is total number of orders.

- Step 23: In the "Fact Table" the Index column was added starting from 1 and renamed to "Order ID", and data typed was changd to text. It will be used to identify the number of sales.
- Step 24: Card visual was selected together with "Order ID" column where distinct columns were counted.

<img width="64" height="47" alt="Orders" src="https://github.com/user-attachments/assets/c83ce956-bf53-4803-bdab-1b7299357472" />

Question 7: Show Sales/Profit/Discount/Net Sales/All remaining fields for each order that could be filtered using visual filters.

- Step 25: A table visual was selected together with all columns from "Fact Table". All columns are not summarised.
- Step 26: Four slicers were added to the report together with the "Date", "Customer Name", " Product Name" and "Promotion Name" to filter the table.
- Step 27: Since the "Fact Table" cannot filter dimension tables and effect slicers, a new measure Sum Dim = SUM('Fact Table'[Net Sales New]) was added to the filter of each slicer (when the value is not blank).

<img width="600" height="337" alt="Slicer 1" src="https://github.com/user-attachments/assets/d4bc50d8-3074-44ee-b878-288735673973" />
<img width="593" height="328" alt="Slicer2" src="https://github.com/user-attachments/assets/1de42a22-ab02-475b-9533-c88b0d21eb30" />

Question 8: Show sales by different cities.

- Step 28: Map visual was used. The data category for the "City" column in "Dim Customer" table was changed to "City". Bubble size was definied by "Sum of Net Sales".

<img width="538" height="288" alt="City" src="https://github.com/user-attachments/assets/51396b5d-2d34-4b12-aa50-dbef62a768fa" />
