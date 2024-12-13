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

## End-to-End Implementation
> Step-1: Review Business Requirements Document(BRD)

> Step-2: Data Gathering by connecting Data source with Power BI Desktop. 

> Step-3: Analysing tables and relations to model data

> Step-4: Data Cleaning and transformation using Power Query Editor with DAX (Data Analysis Expressions). 

> Step-5: Developing an Interactive BI Dashboard / Report.

## Report:
![reportp1](https://github.com/mujahid777/RBC-Bank-Churn-Analysis/blob/main/Report%20page%201.png))
![reportp2](https://github.com/mujahid777/RBC-Bank-Churn-Analysis/blob/main/Report%20page%202.png)

## Dashboard:
![Dashboard](https://github.com/mujahid777/RBC-Bank-Churn-Analysis/blob/main/Dashboard.png)


## DAX calculations

> **Total Customers** = count(Bank_Churn[CustomerId])

> **Active Customers** = CALCULATE(count(Bank_Churn[CustomerId]),
                                    ActiveCustomer[ActiveCategory] = "Active Member")

> **Inactive Customers** = CALCULATE(count(Bank_Churn[CustomerId]),
                                       ActiveCustomer[ActiveCategory] = "Inactive Member")

> **Credit Card Holders** = CALCULATE(count(Bank_Churn[CustomerId]),     
                                         CreditCard[Category] = "Credit Card Holder")

> **Non Credit Card Holders** = CALCULATE(count(Bank_Churn[CustomerId]), 
                                                CreditCard[Category] = "Non Credit Card Holder")

> **Exit Customers** = CALCULATE([Total Customers], 
                                 ExitCustomer[ExitCategory] = "Exit")

> **Retain Customers** = CALCULATE([Total Customers], 
                                    ExitCustomer[ExitCategory] = "Retain")

> **Previous Month Exit Customers** = calculate([Exit Customers],
                                                             PREVIOUSMONTH(DateMaster[Date]))
> **Churn %** = 
var EC = [Exit Customers]
var TC = [Total Customers]
var churnper = DIVIDE(EC,TC)
RETURN churnper

> **Credit Type** = SWITCH(true(), 
Bank_Churn[CreditScore] >= 800 && Bank_Churn[CreditScore]<= 850, "Excellent",
Bank_Churn[CreditScore] >= 740 && Bank_Churn[CreditScore]<= 799, "Very Good",
Bank_Churn[CreditScore] >= 670 && Bank_Churn[CreditScore]<= 739, "Good",
Bank_Churn[CreditScore] >= 580 && Bank_Churn[CreditScore]<= 699, "Fair",
Bank_Churn[CreditScore] >= 300 && Bank_Churn[CreditScore]<= 579, "Poor")


## Strategies for customer retention.

Here are some effective strategies for customer retention:

1. Add dimensions such as customer complaints, transaction declines, or service issues to correlate with churn events.

2. Include data on retention strategies (e.g., customers retained after a churn warning call) to assess effectiveness.

3. To effectively target interventions, it's crucial to analyze churn rates at different stages of the customer lifecycle.

4. Identify customers who have become inactive and measure the rate at which they leave.

5. Investigate seasonal factors (e.g., holidays, tax season) causing spikes churn.













