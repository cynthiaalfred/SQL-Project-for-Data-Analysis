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
