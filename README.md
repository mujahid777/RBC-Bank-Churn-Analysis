#  RBC-Bank-Churn-Analysis
## Problem Statement

RBC bank faces a persistent challenge of customer churn, leading to financial losses and decreased customer satisfaction. Understanding the factors that drive customers to leave is critical to devising strategies for customer retention.

### Objective :-

**This project aims to:**
1. Analyse customer churn data to identify key factors influencing customer attrition.
2. Provide actionable insights to help RBC Bank proactively target customers at risk of leaving, thereby improving retention efforts and reducing churn-related losses.
3. This project aims to analyse the customer churn rate for the bank because it is useful to understand why customers leave.
4. The analysis aims on identifying various KPIs such as Inactive customers, Retain Customers, Exit Customers, and the underlying patterns like previous month exit customers vs. current 
   month exit customers, customers churn by credit type, customer churn by gender, churn %, customers by geographic location etc.

# Dashboard:
![Dashboardp1](https://github.com/mujahid777/RBC-Bank-Churn-Analysis/blob/main/DashboardP1.png)
![Dashboardp2](https://github.com/mujahid777/RBC-Bank-Churn-Analysis/blob/main/Dashboardp2.png)

## In-Depth Project Flow

### 1. Business Requirement Document (BRD)
The BRD outlines the objectives, project scope, and detailed requirements for the RBC Customer Churn Analysis. This document serves as a blueprint for the entire project, ensuring all stakeholders are aligned and the project goals are clear.

**Data Dictionary**
•	RowNumber—corresponds to the record (row) number and has no effect on the output.
•	CustomerId—contains random values and has no effect on customer leaving the bank.
•	Surname—the surname of a customer has no impact on their decision to leave the bank.
•	CreditScore—can have an effect on customer churn, since a customer with a higher credit score is less likely to leave the bank.

**Credit score:**
•	Excellent: 800–850
•	Very Good: 740–799
•	Good: 670–739
•	Fair: 580–669
•	Poor: 300–579

•	Geography—a customer’s location can affect their decision to leave the bank.
•	Gender—it’s interesting to explore whether gender plays a role in a customer leaving the bank.
•	Age—this is certainly relevant, since older customers are less likely to leave their bank than younger ones.
•	Tenure—refers to the number of years that the customer has been a client of the bank. Normally, older clients are more loyal and less likely to leave a bank.
o	Balance—also a very good indicator of customer churn, as people with a higher balance in their accounts are less likely to leave the bank compared to those with lower balances.
o	NumOfProducts—refers to the number of products that a customer has purchased through the bank. 
o	HasCrCard—denotes whether or not a customer has a credit card. This column is also relevant, since people with a credit card are less likely to leave the bank.
•	1 represents credit card holder
•	0 represents non credit card holder
o	IsActiveMember—active customers are less likely to leave the bank.
•	1 represents Active Member
•	0 represents Inactive Member
o	Estimated Salary—as with balance, people with lower salaries are more likely to leave the bank compared to those with higher salaries.
o	Exited—whether or not the customer left the bank.
  0 represents Retain 
  1 represents Exit
o	Bank DOJ — date when the Customer associated/joined  with the bank.


### 2. Data Gathering
In this phase, data is collected from various sources provided by RBC. This involves extracting data relevant to customer demographics, transaction history, service usage, and churn status.

Please use the following data assets to pull the data related to Bank customer and associated details.
o	ActiveCustomer 
o	Bank_Churn
o	CreditCard
o	CustomerInfo
o	ExitCustomer
o	Gender
o	Geography

### 3. Data Cleaning/Data Transformation
Raw data often contains inconsistencies and missing values. In this step, the data is cleaned and transformed to ensure accuracy and reliability. This involves handling missing values, removing duplicates, and standardizing data formats.

### 4. Data Modeling
Data modeling involves structuring the cleaned data into a format suitable for analysis. This step includes defining relationships between different data entities and creating a data schema that supports efficient querying.


### 5. DAX Functions
DAX (Data Analysis Expressions) functions are used to perform calculations and aggregations on the data. These functions help in creating calculated columns, measures, and complex data models that drive the analysis.


**Total Customers** = count(Bank_Churn[CustomerId])

**Active Customers** = CALCULATE(count(Bank_Churn[CustomerId]),
                                    ActiveCustomer[ActiveCategory] = "Active Member")

**Inactive Customers** = CALCULATE(count(Bank_Churn[CustomerId]),
                                       ActiveCustomer[ActiveCategory] = "Inactive Member")

**Credit Card Holders** = CALCULATE(count(Bank_Churn[CustomerId]),     
                                         CreditCard[Category] = "Credit Card Holder")

**Non Credit Card Holders** = CALCULATE(count(Bank_Churn[CustomerId]), 
                                                CreditCard[Category] = "Non Credit Card Holder")

**Exit Customers** = CALCULATE([Total Customers], 
                                 ExitCustomer[ExitCategory] = "Exit")

**Retain Customers** = CALCULATE([Total Customers], 
                                    ExitCustomer[ExitCategory] = "Retain")

**Previous Month Exit Customers** = calculate([Exit Customers],
                                                             PREVIOUSMONTH(DateMaster[Date]))
**Churn %** = 
var EC = [Exit Customers]
var TC = [Total Customers]
var churnper = DIVIDE(EC,TC)
RETURN churnper

**Credit Type** = SWITCH(true(), 
Bank_Churn[CreditScore] >= 800 && Bank_Churn[CreditScore]<= 850, "Excellent",
Bank_Churn[CreditScore] >= 740 && Bank_Churn[CreditScore]<= 799, "Very Good",
Bank_Churn[CreditScore] >= 670 && Bank_Churn[CreditScore]<= 739, "Good",
Bank_Churn[CreditScore] >= 580 && Bank_Churn[CreditScore]<= 699, "Fair",
Bank_Churn[CreditScore] >= 300 && Bank_Churn[CreditScore]<= 579, "Poor")






