<h1> Tokopedia Promo Efficiency & User Retention Analysis </h1>

## 1. Project Overview
This project analyzes e-commerce business data from Tokopedia (January 2023 – December 2024) to extract insights, improve decision-making, and identify key trends regarding promotional budget allocation and user retention. The primary focus is to **address the declining promotional budget efficiency (CLV:CAC ratio) and stagnant user Repeat Order Rate (ROR) caused by aggressive discount campaigns ("burn rate") and post-purchase operational friction**.

Key Objectives:
- Objective 1: Validate and clean multi-table e-commerce datasets (handling naming standardization, business-logic missing values, duplicate transactions, extreme/negative anomalies, and relational integrity).
- Objective 2: Optimize promotional budget allocation to ensure subsidies drive sustainable long-term Customer Lifetime Value (CLV) rather than one-off discount-seeking transactions.
- Objective 3: Identify key drivers of user retention—both promotional patterns and first-order operational experiences—to increase the Repeat Order Rate (<= 90 days) from the current 68.31% baseline to its optimal potential.

## 2. Data Sources
- [transactions.csv](data/raw/transactions.csv) & [clean_transactions.csv](data/cleaned/clean_transactions.csv) - Transaction records (2023–2024) detailing order dates, total GMV, promo amounts, voucher types, payment methods, product categories, and campaign period flags.
- [users.csv](data/raw/users.csv) & [clean_users.csv](data/cleaned/clean_users.csv) – Customer demographic and account profiles, including join dates, age, gender, location/province, device types, and acquisition channels (organic, ads, referral, affiliate).
- [deliveries.csv](data/raw/deliveries.csv) & [clean_deliveries.csv](data/cleaned/clean_deliveries.csv) – Logistics and shipment records covering courier names, service types, shipping zones, promised SLA days, actual dispatch/delivery dates,delivery statuses, and ratings.
- [customer_service_tickets.csv](data/raw/customer_service_tickets.csv) & [clean_customer_service_tickets.csv](data/cleaned/clean_customer_service_tickets.csv) – Post-purchase complaint logs containing ticket categories, communication channels, resolution statuses, resolution times, and CSAT scores.
- [sellers.csv](data/raw/sellers.csv) & [clean_sellers.csv](data/cleaned/clean_sellers.csv) – Merchant profiles including store ratings, official store status, primary product categories, and average response times.

## 3. Technologies Used
- Programming Language: Python (Pandas, NumPy)
- Visualization: Matplotlib, Seaborn
- Interactive Dashboard: Tableau
- Version Control: Git
- Others: Jupyter Notebook / Google Colab

## 4. Project Structure

```
├── README.md          <- The README for developers using this project.
|
├── data
│   ├── raw            <- Data from third party sources (users, transactions, deliveries, sellers, tickets).
│   └── cleaned        <- The data that has been cleaned and flagged for anomalies.
│
├── notebooks          <- Jupyter notebooks for data cleaning and exploratory data analysis:
│   ├── tokopediaAnalysis_dataCleaning.ipynb       <- End-to-end data cleaning & validation pipeline.
│   └── tokopediaAnalysis_dataAnalysis_Cleaner.ipynb <- Cohort ROR initialization & EDA.
│
├── reports            <- Generated analysis as PowerPoint, PDF, LaTeX, etc.
|   ├── slide          <- Generated PowerPoint
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with pip freeze > requirements.txt
│
└── src                <- Source code for use in this project.

```

## 5. Summary of Finding
### 5.1 Business Insight
- **Acquisition Channel & Demographic Efficiency:** Promo Repeat Order Rate (ROR) is relatively uniform across acquisition channels and demographic segments (~68%–71%). However, the **Ads** channel absorbs the highest promo cost per user while yielding the lowest CLV:CAC proxy ratio, whereas **Referral** and **Organic** channels generate much healthier long-term value at a lower subsidy cost.
- **Promo Usage Patterns:** Customers acquired during major campaign periods (WIB/Flash Sales) exhibit lower retention compared to regular-day buyers, indicating a high influx of seasonal discount seekers. Among promo types, **Free Shipping (`free_ongkir`)** achieves the highest retention with the lowest average subsidy cost per user, while **Electronics** and **Fashion** categories deliver the highest GMV-to-Promo return.
- **Root Cause of Budget Inefficiency (Over-Subsidy):** The vast majority of promotional transactions use normal discount amounts and generate a healthy GMV return. However, the overall promo budget is heavily drained by a small fraction of extreme-discount transactions, including a system validation loophole where promo deductions exceed the total transaction amount (`promo_amount > total_amount`).
- **Root Cause of Retention Bottleneck (First-Order Experience):** Stagnant retention is driven primarily by post-purchase operational friction rather than promo mechanics. Customers who experience **failed deliveries**, **SLA delays**, or **CS complaints** on their very first order suffer a drastic drop in ROR. Conversely, users who experience a smooth, complaint-free, and on-time first order achieve a significantly higher ROR (~73.5%).

### 5.2 Actionable Recommendation
- **Enforce Promo Capping & Checkout Rule Validation:** Implement a hard cap on maximum promo discounts alongside minimum basket size requirements, and immediately patch the checkout rule engine to block vouchers from exceeding total transaction values. This stops severe budget leakage while preserving healthy GMV returns.
- **Launch a "First-Order SLA Guarantee" Program:** Prioritize operational handling for first-time buyers by routing their discovery to high-rated/Official stores, assigning top-performing couriers to prevent SLA breaches, and providing a fast-track CS resolution lane for first-order tickets. Eliminating first-order friction is the most effective lever to lift ROR toward its ~73.5% potential and protect long-term GMV.
- **Shift Campaign Subsidies to Tiered Free Shipping & Referral Growth:** Reduce one-off deep discounts during major campaigns (WIB) and replace them with bundled **Free Shipping vouchers** unlocked on a user's 2nd and 3rd purchases. Reallocate inefficient Ads spend toward strengthening the **Referral** program to acquire high-CLV users.
- **Strengthen Internal Data Governance:** Implement automated schema and business-rule validations in the data pipeline to prevent duplicate `order_id` logging, negative transaction values, and chronological mismatches (`order_date < join_date`).

## 6. Contact The Developers
- Name: Reyner Elazaro Tampubolon
- Email: reynerelazaro@gmail.com


- Name: Muhammad Aldi Riansyah
- Email: m.aldiriansyahhh2@gmail.com