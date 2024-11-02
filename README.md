# LITA-CAPSTONE-PROJECT-CUSTOMER-DATA

This where I document my capstone project for my LITA Data Analysis class with the incubator hub. Here, I analysed the customer data provided.

[Project Title](#project-title)

[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools Used](#tools-used)

[Data Cleaning and Preparation](#data-cleaning-and-preparation)

[Exploratoratory Data Analysis](#exploratoratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

[Observation from Visualizations](#observation-from-visualizations)

[Recommendation from Analysis](#recommendation-from-analysis)


### Project Title: Sales Data Analysis

### Project Overview
This data analysis project was done on a customer data where customers subscribes to service for a particular time. The customer pays an amount of money to have access to the service for a duration. Customer have three types of subscription to subscribe too and they can also cancel the subscription.

### Data Sources
Data was provided by the Incubator hub to be used for the project. The Primary data used here is customer data.xlsx

### Tools Used
- Microsoft Excel : This was used for:
  1.  data cleaning
  2.  analysis 
  3.  creation of pivot tables
- Structured Query Language - This was used to query the data to provide data answers and trends.
  
- Power BI - This was used to create various data visualizations.
  
- GitHub- This was used to document the project.
  
### Data Cleaning and Preparation
Data was cleaned using microsoft excel. Duplicate rows were deleted by using the data ribbon. Data was filtered by column to detect blank spaces. The column names were formatted properly.

### Exploratoratory Data Analysis
EDA involved answering some questions about the sales data such as;
- what are the subsription patterns?
- What is the average subsription duration and the most popular subscription types?
- What is the total number of customers from each region?
- What is total revene by subscription type?
- What are the top 3 regions by subscription cancellations?

 ### Data Analysis
  This is where I include excel formulas, basic lines of queries from SQL and some 
 DAX expressions from PowerBi used during my analysis;
 
 SQL

``` SQL
create database LITA_project_2
select * from [dbo].[LITA Capstone Customer Dataset]

-----customer by region
select count([CustomerName]) as Customer, [Region] from [dbo].[LITA Capstone Customer Dataset]
group by [Region]

-----most popular subscription
select top 1 count([CustomerName]) as Customer, [SubscriptionType] from [dbo].[LITA Capstone Customer Dataset]
group by [SubscriptionType]

alter table [dbo].[LITA Capstone Customer Dataset]
add duration_sub as datediff(month,[SubscriptionStart],[SubscriptionEnd])
Select*from [dbo].[LITA Capstone Customer Dataset]

-----average subscription duration
Select AVG(duration_sub) as average_duration from [dbo].[LITA Capstone Customer Dataset]

-----customer with subscription duration more than 12 months

Select [CustomerName] from [dbo].[LITA Capstone Customer Dataset]
where duration_sub >12

-----total revenue by subscription type

Select sum([Revenue]) as subsription_revenue , [SubscriptionType] from [dbo].[LITA Capstone Customer Dataset]
group by [SubscriptionType]

-----customer cancelled within 6 months
Select [CustomerName] from [dbo].[LITA Capstone Customer Dataset]
where duration_sub <=6


select * from [dbo].[LITA Capstone Customer Dataset]

----top 3 regions with cancelled subscription
select top 3 count([Canceled]) as cancellation ,[Region]  from [dbo].[LITA Capstone Customer Dataset]
where [Canceled] = 0
group by [Region]
order by 1 desc
```
Excel
```excel
Subsription duration =F2-E2
Average subsription duration =AVERAGE(I2:I33788)
Popular subscription type =COUNTIF($D$2:$D$33788,D2), =MAX(O4,O5,O6)
```
PowerBi
```powerbi
subsription duration =[SubscriptionEnd] - [SubscriptionStart
Cancellation conditional column- if cancelled equals TRUE Then 1 else 0
 Table.AddColumn(#"Changed Type", "Cancellation", each if [Canceled] = true then 1 else 0)
```

### Data Visualization
Pivot table
![Screenshot (22)](https://github.com/user-attachments/assets/241de696-faa8-40a4-a1ab-000844620a75)

Power bi Visualization
![Screenshot (23)](https://github.com/user-attachments/assets/9543c64e-e486-4c5c-930f-87c0e5ba866c)

### Observation from Visualizations
Looking at the subscription trends, the highest revenue was from the basic subscription type with a total revenue of 33,776,735 and the least revenue from the standard subscription type with a total revenue of 16,864,376. The region with the highest revenue is the East with revenue of 16,958,763 and only the basic subscription type is subscribed to in the East. Only the basic subscription type is subscribed to in the North which has the least total revenue of 16,817,972. Only the premium is subsribed to in the South and only the standard is subscribed to in the West. The top 5 customers by revenue are Liam,Mike,Sophia,Nina and Anna with revenues of 343744,3427436,3414995,3399895 and 3398288 respectively.

The region with the highest calculation is the East with a total cancellation of 8488

