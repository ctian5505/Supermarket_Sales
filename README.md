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

### Adding date table (Table View)
```R
Calendar = CALENDAR(MIN(Fact_Sales[Date]), MAX(Fact_Sales[Date]))

Year = FORMAT('Calendar'[Date], "yyyy")

Month = FORMAT('Calendar'[Date], "Mmm")

MonthNo = FORMAT('Calendar'[Date], "m") //Use to sort the month
```

### Creating Relationship (Model View)
![Relationships Model View](https://github.com/ctian5505/Supermarket_Sales/blob/main/relationship.png)

### Creating Measures 
```R
Average_Rating = AVERAGE(Fact_Sales[Rating])

// Calculate the average rating
```


```R
Branch_Count = COUNT(Dim_Branch[Branch]) 

// Count the branch
```

```R
Full_Date_Name = FORMAT(SELECTEDVALUE('Calendar'[Date]), "Mmmm dd yyyy")

// Display the full date name (used in tool tip)
```

```R
Gross_Income = SUM(Fact_Sales[gross_income])

// Calculate the gross income
```

```R
Product_Count = COUNT(Dim_Product_Line[Product_line]) 

// Count the product
```

```R
Quantity_Sold = SUM(Fact_Sales[Quantity]) 

// Calculate the total quantity sold
```

```R
Revenue = SUM(Fact_Sales[Total]) 

// Calculate the total revenue
```

```R
Transaction_Count = COUNT(Fact_Sales[Invoice_ID])

// Count the transaction
```
*Adding Reset Button Using Bookmark*
![Reset](https://github.com/ctian5505/Supermarket_Sales/blob/main/Default.png)

*Adding Tool Tip*
![Daily Sales Tool Tip](https://github.com/ctian5505/Supermarket_Sales/blob/main/Daily_Sales_Tp.png)
![Daily Sales Tool Tip](https://github.com/ctian5505/Supermarket_Sales/blob/main/Revenue%20by%20Product%20Line%20TP.png)
![Daily Sales Tool Tip](https://github.com/ctian5505/Supermarket_Sales/blob/main/Revenue%20by%20City%20TP.png)
![Daily Sales Tool Tip](https://github.com/ctian5505/Supermarket_Sales/blob/main/TP%20ALL.png)




# Final Output
![Super Market Sales Dashboard](https://github.com/ctian5505/Supermarket_Sales/blob/main/Supermarket%20sales_page-0001.jpg)
