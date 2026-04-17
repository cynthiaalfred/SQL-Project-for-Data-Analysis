# SQL-Project-for-Data-Analysis
Practised real-world case study analysing Swiggy sales data to uncover customer behaviour, sales trends, and key business insights.

### Step by Step Project

To import data
- Right click on Databases > New Database > Update Database Name > click ok
- This will execute and create a new database 
- Select new database > right click > select Tasks > select Import Flat File > brose and select file > update table name 

![](https://github.com/cynthiaalfred/SQL-Project-for-Data-Analysis/blob/main/Operation%20Failed.png)

As there are two errors -  the combo for the string cannot be converted to type nvarchar for Dish_Name 
-(as the values in column Dish Name is very large and multiple characters used - its a large stored value)
- Changed the Dish_Name to varchar(200)
- Similarly I've renamed other data type nvarchar(50) to varchar (150)

> operation complete and result is success > close the tab as the data is now uploaded.
