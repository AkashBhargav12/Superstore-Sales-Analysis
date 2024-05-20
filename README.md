# SuperStore Sales Analysis


![Superstore Sales analysis](Assests/Images/Banner Image.png)




# Table of Contents

- [Objective](#objective)
- [Data Source](#data-source)
- [Stages](#stages)
- [Design](#design)
  - [Mockup](#mockup)
  - [Tools](#tools)
- [Development](#development)
  - [Data Exploration](#data-exploration)
  - [Data Cleaning](#data-cleaning)
  - [Transform the Data](#transform-the-data)
- [Testing](#testing)
  - [Data Quality Tests](#data-quality-tests)
- [Visualization](#visualization)
  - [Results](#results)
- [Analysis](#analysis)
  - [Findings](#findings)
  - [Validation](#validation)
  - [Discovery](#discovery)
- [Recommendations](#recommendations)
  - [Potential ROI](#potential-roi)
  - [Potential Courses of Actions](#potential-courses-of-actions)
- [Conclusion](#conclusion)


# Objective

The primary objective of this analysis is to derive insights from the Superstore's sales data to answer the following key questions:
1. What is the total revenue generated by the store?
2. Which category of products contributes the most to sales?
3. How has the sales trend been for the past year?
4. Which region has the highest sales and which one has the lowest?
5. What is the average profit margin of the store?

## User Story

As the General Manager, I want to identify the bestselling products and the recent trends, so that I can decide on which products would be best to run marketing campaigns on to generate a good ROI. 


# Data Source

The data for this analysis is sourced from the Superstore Sales dataset, which includes detailed information on orders, returns, users, and various dashboards and pivot tables. The dataset comprises multiple sheets:
- Description and Questions
- Orders
- Returns
- Users

The data is sourced from Kaggle (an Excel extract), [see here to find it](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)

# Stages

The project is divided into several stages:
1. Data Exploration
2. Data Cleaning
3. Data Transformation
4. Testing
5. Visualization
6. Analysis
7. Recommendations
8. Conclusion


# Design

## Dashboard components required 
What should the dashboard contain based on the requirements provided?

- What is the total revenue generated by the store?
- Which category of products contributes the most to sales?
- How has the sales trend been for the past year?
- Which region has the highest sales and which one has the lowest?
- What is the average profit margin of the store?

## Mockup

The design phase includes creating mockups to visualize the expected output of the dashboards and reports. Mockups help in understanding the layout and design elements that will be used in the final visualizations.

Some of the data visuals that may be appropriate in answering our questions include:

1. Line Chart
2. Bar Chart
3. Scorecards
4. Pie Chart 


![Dashboard-Mockup](Assests/Images/Mockup.png)

## Tools Used

This project analysis has been conducted entirely within **Excel** to showcase the depth of knowlege with the toold and the expertise.


# Development

## Data Exploration Steps

How can we approach the problem to create a solution from start to finish?

  1. Get the data from a reliable data source
  2. Explore the data in Excel to check for any errors that standout
  3. Create addtional columns using to find the distinct orders, return rate, and distinct return rate
  4. Create pivot tables to summarise customers and order data, sales data and product data
  5. Create pivot charts to visualise the data
  6. Create slicers to ease the navigation through the data
  7. Arrange the visualisation dashboards
  8. Generate the findings based on the insights
  9. Write the documentation + commentary
  10. Publish the insights generated


## Data exploration notes

This is the stage where we scan the data for errors, inconcsistencies, bugs, weird and corrupted characters etc. 

The data exploration stage involves understanding the structure of the raw data. The key findings from each sheet in the SuperStoreUS-2015.xlsx file are summarized below:

1. Orders Sheet: Contains detailed order information including sales, profit, product categories, and customer details.
2. Returns Sheet: Lists the orders that were returned.
3. Users Sheet: Provides information on regional managers.

Additionally the sheets contain the following columsn;

- Row ID
- Order Priority
- Discount
- Unit Price
- Shipping Cost
- Customer ID
- Customer Name
- Ship Mode
- Customer Segment
- Product Category
- Product Sub-Category
- Product Container
- Product Name
- Product Base Margin
- Country
- Region
- State or Province
- City
- Postal Code
- Order Date
- Ship Date
- Profit
- Quantity ordered new
- Sales
- Order ID
- Return Status
- Region
- Manager

What are the initial observations with this dataset? What's caught our attention so far?

1. The dataset includes detailed order information with relevant dates, sales and profit figures. The initial exploration reveales that the quality of the data is high and we have everything we need to perform the analysis.
2. The Returns and Users sheets contains data that can be linked to orders through 'Order ID' and 'Region'.
3. There are some blanks and irregular data that needs to be cleaned before conducting the analysis. 
4. There is a need to calculate the dintinct number of orders and returns.


## Data cleaning 
- What do we expect the clean data to look like? What should it contain? What contraints should we apply to it?

The aim is to refine the dataset to ensure it is structured and ready for analysis. 

The cleaned data should meet the following criteria and constraints:

1. Removing any duplicate entries in the orders IDs
2. Handling any missing values in critical columns like sales and profit

Below is a table outlining the our cleaned dataset:

| Sheet | Number of Rows | Number of Columns |
| --- | --- | --- |
| --- | --- |
| **Orders** | 1952 | 25
| --- | --- |
| --- | --- |
| **Returns** | 1635 | 2 |
| --- | --- |
| --- | --- |
| **Users** | 5 | 2 |


### Transform the data

Before we can begin analysing the data it is necessary to transform the data with a few addtional columns to make it more coherent and usable.

The below additional columns have been created using the formulae shown :

Distinct Customer Count
```sql
=IF(COUNTIF(G$2:G2,G2)=1,"New Customer","Returning Customer")
```

Customer Count Distinct
```sql
=IF(H2="New Customer",1,0)
```

Order Day
```sql
=TEXT(W2,"ddd")
```

Delivery Days
```sql
=Y2-W2
```

Is Discount
```sql
=IF(C2=0,"No Discount","After Discount")
```

Distinct Order Count
```sql
=IF(COUNTIF(AE$2:AE1953,AE2)=1,1,0)
```

Distinct Return Status
```sql
=IF(AG2="Not Returned",0,1)
```

Further to the above additonal columns, a few other columns have been added from other sheets using the **XLOOKUP** formula to amalgamate all the data on a single sheet to ease the analysis process.

- For Example
Return Status
```sql
=XLOOKUP(AE2,Returns!A:A,Returns!B:B,"Not Returned",0,1)
```


# Testing

To ensure the accuracy and reliability of the data, several tests were conducted:

- Row Count Check: Verify the number of records.
- Column Count Check: Ensure all necessary columns are present.
- Data Type Check: Confirm appropriate data types for each column.
- Duplicate Check: Ensure all records are unique.

#### Row Count Check

Checked all rows in column A to ensure the count matches the expected number of records (1952)
Formula Used
```sql
=COUNTA(A:A)
```

#### Column Count Check

Checked all columns in row 1 to ensure all 25 columns and the additional added 9 columns are present 
Formula Used
```sql
=COUNTA(1:1)
```
#### Duplicate Check

- Applied Conditonal Formatting to highlight duplicate values to columns that uniquely identify records, such as Order ID (column AE).
- Verified that there were no duplicate entries.

#### Missing Values Check:

Checked 'Sales', 'Profit' and 'Order Date' columns for any missing values and ensured that these critical fields were filled.
Formula Used
```sql
=ISBLANK(U2)
```


# Visualisation

- What does the dashboard look like?

### Customer and Order Analysis

![Customer and Order Analysis](Assests/Images/Customer and order dashboard_Page_1.png)


### Sales Analysis

![Sales Analysis](Assests/Images/Sales Dashboard_Page_1.png)


### Product Analysis

![Product Analysis](Assests/Images/Product Dashboard_Page_1.png)
























