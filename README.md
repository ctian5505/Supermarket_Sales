# Supermarket_Sales
![Super Market Sales Dashboard](https://github.com/ctian5505/Supermarket_Sales/blob/main/Supermarket%20sales_page-0001.jpg)

## Data from kaggle
[Datasets](https://www.kaggle.com/datasets/aungpyaeap/supermarket-sales)

# Objectives
```
- Clean the data
- Upload the data into SQL Server Management Server (SSMS)
- Create a query and upload to POWER BI
- Create a dashboard
```

## STEP 1 : Downloading datasets
```
  - Download the dataset [https://www.kaggle.com/datasets/aungpyaeap/supermarket-sales], saved as CSV
```

## STEP 2 : Uploading into SSMS
###   - Create database
```sql
-- Creating Database
CREATE DATABASE Supermarket_Sales
```
###   - Uploading the CSV file into SSMS as Flat File 

*The file consists of a single table, which is not well-structured because all data is stored in one place. I want to optimize it by designing a proper schema with fact and dimension tables. I also need an SQL query to implement this optimization.*

###   - Creating Query for optimization

```sql
-- Making Dimension Branch
SELECT 
	CASE
		WHEN Branch = 'A' THEN 1
		WHEN Branch = 'B' THEN 2
		WHEN Branch = 'C' THEN 3
	END AS 'Branch_ID',
	Branch
FROM 
	supermarket_sales
GROUP BY
	Branch
```
```sql
	-- Making Dimension City
SELECT
	CASE
		WHEN City = 'Naypyitaw' THEN 1
		WHEN City = 'Yangon' THEN 2
		WHEN City = 'Mandalay' THEN 3
	END AS City_ID,
	City
FROM
	supermarket_sales
GROUP BY
	City
```
```sql
		-- Making Dimension Payment
SELECT 
	CASE
		WHEN Payment = 'Ewallet' THEN 1
		WHEN Payment = 'Cash' THEN 2
		WHEN Payment = 'Credit card' THEN 3
	END AS Payment_ID,
	Payment
FROM 
	supermarket_sales
GROUP BY
	Payment
```
```sql
	-- Making Dimension Customer_type 
SELECT 
	CASE
		WHEN Customer_type = 'Normal' THEN 1
		WHEN Customer_type = 'Member' THEN 2
	END AS Customer_Type_ID,
	Customer_type 
FROM 
	supermarket_sales
GROUP BY
	Customer_type
```
```sql
-- Making Dimension Gender
SELECT 
	CASE
		WHEN Gender = 'Male' THEN 1
		WHEN Gender = 'Female' THEN 2
	END AS Gender_ID,
	Gender
FROM 
	supermarket_sales
GROUP BY
	Gender
```
```sql
	-- Making Dimension Product_line
SELECT 
	CASE
		WHEN Product_line = 'Fashion accessories' THEN 1
		WHEN Product_line = 'Health and beauty' THEN 2
		WHEN Product_line = 'Electronic accessories' THEN 3
		WHEN Product_line = 'Food and beverages' THEN 4
		WHEN Product_line = 'Sports and travel' THEN 5
		WHEN Product_line = 'Home and lifestyle' THEN 6
	END AS Product_line_ID,
	Product_line
FROM 
	supermarket_sales
GROUP BY
	Product_line
```
```sql
	-- Creating Fact Sales
SELECT 
	Invoice_ID,
	CASE
		WHEN Branch = 'A' THEN 1
		WHEN Branch = 'B' THEN 2
		WHEN Branch = 'C' THEN 3
	END AS 'Branch_ID',
	CASE
		WHEN City = 'Naypyitaw' THEN 1
		WHEN City = 'Yangon' THEN 2
		WHEN City = 'Mandalay' THEN 3
	END AS City_ID,
	CASE
		WHEN Customer_type = 'Normal' THEN 1
		WHEN Customer_type = 'Member' THEN 2
	END AS Customer_Type_ID,
	CASE
		WHEN Gender = 'Male' THEN 1
		WHEN Gender = 'Female' THEN 2
	END AS Gender_ID,
	CASE
		WHEN Product_line = 'Fashion accessories' THEN 1
		WHEN Product_line = 'Health and beauty' THEN 2
		WHEN Product_line = 'Electronic accessories' THEN 3
		WHEN Product_line = 'Food and beverages' THEN 4
		WHEN Product_line = 'Sports and travel' THEN 5
		WHEN Product_line = 'Home and lifestyle' THEN 6
	END AS Product_line_ID,
	Unit_price,
	Quantity,
	Tax_5,
	Total,
	CAST(Date AS DATE) AS Date,
	DATEPART(HOUR, Time) AS Time_Hour,
	Payment,
	cogs,
	gross_margin_percentage,
	gross_income,
	Rating
  FROM 
	supermarket_sales
```

## STEP 3 : Power BI
![Power Query](https://github.com/ctian5505/Supermarket_Sales/blob/main/Screenshot%202025-03-07%20163630.png)
*Upload the query and clean*


