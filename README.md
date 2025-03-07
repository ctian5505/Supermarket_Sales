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
### - Create database
```sql
-- Creating Database
CREATE DATABASE Supermarket_Sales
```
### - Uploading the CSV file into SSMS as Flat File 

### The file consists of a single table, which is not well-structured because all data is stored in one place. I want to optimize it by designing a proper schema with fact and dimension tables. I also need an SQL query to implement this optimization.
