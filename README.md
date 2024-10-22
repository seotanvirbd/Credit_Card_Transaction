# From CSV to PostgreSQL to Power BI: Analyzing Credit Card Transactions and Customer Reports

![Project Banner](https://github.com/seotanvirbd/Credit_Card_Transaction/blob/main/credit_card_transcation_dashboard.png)

## 📊 Project Overview

This comprehensive data analysis project demonstrates the end-to-end process of transforming raw CSV data into actionable insights using PostgreSQL and Power BI. By analyzing credit card transactions and customer reports, we've created interactive dashboards that provide real-time insights into key performance metrics and trends.

### 🎯 Project Objective

To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.

## 🚀 Key Features

- Data pipeline from CSV to PostgreSQL
- Advanced SQL queries for data transformation
- Interactive Power BI dashboards
- Credit card transaction analysis
- Customer report visualization
- Real-time performance metrics

## 💡 Project Insights (Week 53 - 31st Dec)

### Week-over-Week Changes
- Revenue increased by 28.8%
- Total Transaction Amount and Count increased significantly
- Customer count showed notable growth

### Year-to-Date Overview
- Overall revenue: 57M
- Total interest: 8M
- Total transaction amount: 46M
- Gender-based revenue contribution:
  - Male customers: 31M
  - Female customers: 26M
- Credit card type contribution:
  - Blue & Silver cards: 93% of overall transactions
- Top contributing states:
  - TX, NY & CA: 68% of total contribution
- Overall Activation rate: 57.5%
- Overall Delinquent rate: 6.06%

## 🛠️ Technologies Used

- PostgreSQL
- Power BI
- Python (for data preprocessing)
- DAX (for advanced calculations in Power BI)

## 📈 Dashboards

### Credit Card Transaction Report
![Credit Card Transaction Dashboard](https://github.com/seotanvirbd/Credit_Card_Transaction/blob/main/credit_card_transcation_dashboard.png)

### Credit Card Customer Report
![Credit Card Customer Dashboard](https://github.com/seotanvirbd/Credit_Card_Transaction/blob/main/credit_card_customer_report_dashboard.png)

## 🔍 Detailed Analysis

### Revenue Analysis
- Total revenue reached 56.5M
- Interest earnings totaled 8.0M
- Transaction amount summed up to 45.5M

### Customer Segmentation
- Age-based revenue distribution
- Income group analysis
- Education level impact on spending

### Geographical Insights
- State-wise revenue breakdown
- Urban vs. Rural spending patterns

### Card Usage Patterns
- Chip vs. Swipe vs. Online transactions
- Card category preferences

## 🔧 Implementation Details

### Data Import Process
```sql
-- Example SQL query for data import
CREATE TABLE cc_detail (
    Client_Num INT,
    Card_Category VARCHAR(20),
    -- ... other columns
);

COPY cc_detail
FROM '/path/to/credit_card.csv' 
DELIMITER ',' 
CSV HEADER;
```

### DAX Queries for Advanced Metrics
```dax
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]

Current_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)
```
# SQL and DAX Queries for Credit Card Analysis

This document contains the SQL queries used for data import and the DAX formulas used in Power BI for advanced calculations in our credit card analysis project.

## SQL Queries

### Creating the Database

```sql
-- Create a database 
CREATE DATABASE ccdb;
```

### Creating Tables

#### Credit Card Details Table

```sql
CREATE TABLE cc_detail (
    Client_Num INT,
    Card_Category VARCHAR(20),
    Annual_Fees INT,
    Activation_30_Days INT,
    Customer_Acq_Cost INT,
    Week_Start_Date DATE,
    Week_Num VARCHAR(20),
    Qtr VARCHAR(10),
    current_year INT,
    Credit_Limit DECIMAL(10,2),
    Total_Revolving_Bal INT,
    Total_Trans_Amt INT,
    Total_Trans_Ct INT,
    Avg_Utilization_Ratio DECIMAL(10,3),
    Use_Chip VARCHAR(10),
    Exp_Type VARCHAR(50),
    Interest_Earned DECIMAL(10,3),
    Delinquent_Acc VARCHAR(5)
);
```

#### Customer Details Table

```sql
CREATE TABLE cust_detail (
    Client_Num INT,
    Customer_Age INT,
    Gender VARCHAR(5),
    Dependent_Count INT,
    Education_Level VARCHAR(50),
    Marital_Status VARCHAR(20),
    State_cd VARCHAR(50),
    Zipcode VARCHAR(20),
    Car_Owner VARCHAR(5),
    House_Owner VARCHAR(5),
    Personal_Loan VARCHAR(5),
    Contact VARCHAR(50),
    Customer_Job VARCHAR(50),
    Income INT,
    Cust_Satisfaction_Score INT
);
```

### Importing Data

#### Importing Credit Card Details

```sql
COPY cc_detail
FROM '/path/to/credit_card.csv' 
DELIMITER ',' 
CSV HEADER;
```

#### Importing Customer Details

```sql
COPY cust_detail
FROM '/path/to/customer.csv' 
DELIMITER ',' 
CSV HEADER;
```

### Importing Additional Data (Week 53)

#### Additional Credit Card Details

```sql
COPY cc_detail
FROM '/path/to/cc_add.csv' 
DELIMITER ',' 
CSV HEADER;
```

#### Additional Customer Details

```sql
COPY cust_detail
FROM '/path/to/cust_add.csv' 
DELIMITER ',' 
CSV HEADER;
```

## DAX Formulas

### Age Group Calculation

```dax
AgeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[customer_age] < 30, "20-30",
    'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
    'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
    'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
    'public cust_detail'[customer_age] >= 60, "60+",
    "unknown"
)
```

### Income Group Calculation

```dax
IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)
```

### Week Number Calculation

```dax
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
```

### Revenue Calculation

```dax
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
```

### Current Week Revenue Calculation

```dax
Current_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)
```

### Previous Week Revenue Calculation

```dax
Previous_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
    )
)
```

These queries and formulas form the backbone of our data processing and analysis in the credit card transaction and customer report project. They demonstrate the power of combining SQL for data management and DAX for advanced calculations in Power BI.
## 📚 Lessons Learned

- Importance of data cleaning and preprocessing
- Effective use of SQL for data transformation
- Power of DAX for complex calculations in Power BI
- Significance of visual storytelling in data analysis

## 🔮 Future Enhancements

1. Implement machine learning models for predictive analytics
2. Integrate real-time data streaming
3. Develop a web application for wider accessibility
4. Expand analysis to include more financial products

## 🤝 Connect with Me

I'm always excited to discuss data analysis, AI, and software development. Feel free to reach out!

- 📱 WhatsApp: [Connect on WhatsApp](https://api.whatsapp.com/send?phone=8801687373830)
- 📘 Facebook: [Tanvir's Facebook](https://www.facebook.com/seotanvirbd)
- 💼 LinkedIn: [Tanvir's LinkedIn](https://www.linkedin.com/in/seotanvirbd/)
- 🎥 YouTube: [Tanvir's YouTube Channel](https://www.youtube.com/@tanvirbinali2200)
- 📧 Email: tanvirafra1@gmail.com
- 🌐 Portfolio & Blog: [SEO Tanvir BD](https://seotanvirbd.com/)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

---

⭐️ If you found this project interesting, please consider giving it a star on GitHub!
