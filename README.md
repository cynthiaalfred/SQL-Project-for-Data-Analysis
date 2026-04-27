# SQL-Project-for-Data-Analysis
Practised real-world case study analysing Swiggy sales data to uncover customer behaviour, sales trends, and key business insights.

### Step by Step Project

To import data
- Right click on Databases > New Database > Update Database Name > click ok
- This will execute and create a new database 
- New database > right click > select Tasks > select Import Flat File > browse and select file > update table name 

![](https://github.com/cynthiaalfred/SQL-Project-for-Data-Analysis/blob/main/Operation%20Failed.png)

(as the values in column Dish Name is very large and multiple characters used - its a large stored value)
- So, I changed the Dish_Name to varchar(200) & renamed other data type nvarchar(50) to varchar (150)
-Once the Operation  was complete and result is success I've close the tab as the data is now uploaded.
- Right click on Swiggy_Data > Refresh > open tables > swiggy_data file is imported.

## Write Query
- select Swiggy Database > right click > new query

```SQL
SELECT * FROM swiggy_data       # * everything from database
```
## Data Cleaning & Validation
### - Null Check Query
```SQL
SELECT
SUM(CASE WHEN State IS NULL THEN 1 ELSE 0 END) AS null_state,
SUM(CASE WHEN City IS NULL THEN 1 ELSE 0 END) AS null_city,
SUM(CASE WHEN Order_Date IS NULL THEN 1 Else 0 END) AS null_Order_date,
SUM(CASE WHEN Restaurant_Name IS NULL THEN 1 ELSE 0 END) AS null_restaurant,
SUM(CASE WHEN Location IS NULL THEN 1 ELSE 0 END) AS null_location, 
SUM(CASE WHEN Category IS NULL THEN 1 ELSE 0 END) AS null_category,
SUM(CASE WHEN Dish_Name IS NULL THEN 1 ELSE 0 END) AS dish,
SUM(CASE WHEN Price_INR IS NULL THEN 1 ELSE 0 END) AS null_price,
SUM(CASE WHEN Rating IS NULL THEN 1 ELSE 0 END) AS null_rating,
SUM(CASE WHEN Rating_Count IS NULL THEN 1 ELSE 0 END) AS null_rating_count
FROM swiggy_data;
```

### Result
![](https://github.com/cynthiaalfred/SQL-Project-for-Data-Analysis/blob/main/Result.png)

### - Blank or Empty Strings Query
```SQL
SELECT*
FROM swiggy_data
WHERE
State = ' ' OR City = '' OR Restaurant_Name = '' OR Location='' OR Category='' OR Dish_Name=''     # '' is space
```
### Result
![](https://github.com/cynthiaalfred/SQL-Project-for-Data-Analysis/blob/main/Result%201.png)

### - Duplicate Detection
```SQL
State, City, Order_Date, Restaurant_Name, Location, Category, Dish_Name, Price_INR, Rating, Rating_Count
```
### Result
![](https://github.com/cynthiaalfred/SQL-Project-for-Data-Analysis/blob/main/Result%202.png)

### - Delete Duplication
```SQL
WITH CTE AS (
SELECT *, ROW_NUMBER() Over(
    PARTITION BY State, City, Order_Date, Restaurant_Name, Location, Category, Dish_Name, Price_INR, Rating, Rating_Count
	ORDER BY (SELECT NULL)
	) AS rn
FROM swiggy_data
)
DELETE FROM CTE WHERE rn>1
```
### Result
![](https://github.com/cynthiaalfred/SQL-Project-for-Data-Analysis/blob/main/Result%203.png)


### Creating Structure of Table

```SQL
--DIMENSION TABLES
--DATA TABLE
CREATE TABLE dim_date(
   date_id INT IDENTITY (1,1) PRIMARY KEY,
   Full_Month DATE,
   Year INT,
   Month INT,
   Month_Name varchar(20),
   Quarter INT,
   Day INT,
   Week INT,
   )

 --dim_location
   --Create Location
   CREATE TABLE dim_location(
   location_id INT IDENTITY (1,1) PRIMARY KEY,
   State varchar (100),
   City varchar(100),
   Location varchar(200)
   )

   SELECT * FROM dim_location

   --dim_restaurant
   --Create Restaurant
   CREATE TABLE dim_restaurant(
   restaurant_id INT IDENTITY (1,1) PRIMARY KEY,
  restaurant_name varchar (200)
  )

  --dim_catogery
  --Create category
  CREATE TABLE dim_category(
  category_id INT IDENTITY (1,1) PRIMARY KEY,
  Category varchar (200)
  )

  --Creare Dish
  CREATE TABLE dim_dish(
  dish_id INT IDENTITY (1,1) PRIMARY KEY,
  dish_name varchar (200)
  )
  
  SELECT * FROM swiggy_data

  --FACT TABLE
  CREATE TABLE fact_swiggy_orders(
  order_id INT IDENTITY (1,1) PRIMARY KEY,

  date_id INT,
  Price_GBP DECIMAL(10,2),
  Rating DECIMAL (4,2),
  Rating_Count INT,

  location_id INT,
  restaurant_id INT,
  category_id INT,
  dish_id INT,

  FOREIGN KEY (date_id) REFERENCES dim_date(date_id),
  FOREIGN KEY (location_id) REFERENCES dim_location(location_id),
  FOREIGN KEY (restaurant_id) REFERENCES dim_restaurant(restaurant_id),
  FOREIGN KEY (category_id) REFERENCES dim_category(category_id),
  FOREIGN KEY (dish_id) REFERENCES dim_dish(dish_id),
  );
```



