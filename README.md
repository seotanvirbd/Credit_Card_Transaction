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
