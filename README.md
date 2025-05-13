# Data Product Factory Exercise

**Purpose:** This Project conatins the solution of two exrcises from `Data Product Factory`. Both the solutions are prepared using `Jupyter Notebook` files.

## Exercise 1: Customer Sales

**Input:** Sales log from 50 Customers are stored in the CSV format in `Notebook\Customer Sales\data\input` path.

**Output:** 
***Files:***
- `All_Customers.csv`
- `Last_Purchase.csv`
***Path:*** `Notebook\Customer Sales\data\output`

### Solution: `Customer_Sales.ipynb`
**Task 1: Combine all files**
* Used `pandas.concat()` method to combine the sales log of each customer.
* Added a new field `Customer_name` to identify the records of each customer.
* Saved the combined dataframe in csv format as `All_Customers.csv`.

**Task 2: Extarct Last Purchase by each customer**
* Loaded the data from `All_Customers.csv` file and stored in the dataframe.
* Replaced `Noon` value in the `Order time` field with `12pm` to standardize the time.
* Combined `Order_date` and `Order_time` fields to create a new filed `Order_datetime`.
* Converted `Order_datetime` data type to datetime format.
* Identified latest datetime of every purchased product for each customer using a `for` loop and `max()` method.
* Saved the Last Purchase dataframe in csv format as `Last_Purchase.csv`.

**Task 3: Distribution Analysis of the products sold**
* Plotted Combined distribution of Products sold using `seaborn.histplot()` method.
* Also plotted separate distribution of each products sold using `matplotlib.pyplot.subplots()` and `seaborn.histplot()` methods.

## Exercise 2: Department and Region Performance

**Input:** Below csv files are stored in the `Notebook\Department and  Region Performance\data\input` folder.

* ***Monthly_budget_cost.csv :*** It stores the monthly budget cost for each Department along with the Region.
* ***Region.csv :*** It stores the list of all the Region and Country where company is situated, along with Regional manager of every Region.
* ***Department.csv :*** It stores the list of all the Departments along with the Region where the department is located and Departmental_manager of each department.
* ***Daily_sales.csv :*** It stores daily sales data of each department. It contains the Sales gross amount, Sales tax amount of the products sold along with the Sales date.

**Outputs:** 
***Files:***
- `Yearly_sales_by_country.csv`
- `Monthly_profit_by_department.csv`
***Path:*** `Notebook\Department and  Region Performance\data\output`

**Database:** `data_product_factory`

**SQL Tables:**
- `daily_sales`
- `region`
- `department`
- `monthly_budget`
- `yearly_sales_by_country`
- `monthly_profit_by_department`

### Solution 1: `SQL_Query.ipynb`
* Loaded data from the input csv files and modified the data types of each field as per the requirement.
* Established connection with localhost instance of mysql database using `sqlalchemy.create_engine()` method.
* Inserted the input data in separate sql tables.


### Solution 2: `Performance.ipynb`

**Task 1: Generate Yearly sales by country**
* Extracted `Year_yyyy` and `Month_yyyymm` from `Sales_date_yyyymmdd` using `to_datetime() and strftime()` methods.
* Grouped `Daily sales` data by `Sales year` and `Department` using `groupby()` method to calculate yearly `Sales gross amount` and `Sales tax amount` for each `Department`.
* Merged the `Grouped Daily sales` data with `Region` and `Department` data using `merge()` method to get the `Region` and `Country` of each `Department`.
* Calculated `Sales Net amount` = `Sales gross amount` - `Sales tax amount`.
* Populated `Yearly_sales_by_country` dataframe with the required fields from the merged data.
* Saved the dataframe in csv format as `Yearly_sales_by_country.csv` and also in sql table `yearly_sales_by_country`.

**Task 2: Generate Monthly profit by department**
* Grouped `Daily sales` data by `Month_yyyymm` and `Department` using `groupby()` method to calculate monthly `Sales gross amount` and `Sales tax amount` for each `Department`.
* Merged the `Grouped Daily sales` data with `Region`, `Department` and `Monthly_budget` data using `merge()` method to get the `Departmental_manager`, `Country` and `Budget_cost` of each `Department`.
* Calculated `Monthly Profit` = `Sales Net amount` - `Budget cost`.
* Populated `Monthly_profit_by_department` dataframe with the required fields from the merged data.
* Saved the dataframe in csv format as `Monthly_profit_by_department.csv` and also in sql table `monthly_profit_by_department`.
