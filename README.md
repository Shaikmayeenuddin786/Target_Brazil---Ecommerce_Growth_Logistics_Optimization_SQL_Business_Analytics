# **Retailer (Brazil E-commerce Analysis)**

### **SQL Analytics | Performance-Logistics-Payments Optimization | Top Business Insights & Recommendations**

<img width="1000" height="666" alt="image" src="https://github.com/user-attachments/assets/a4cd69dc-bf88-4c1d-9c51-2acb73f9a27a" />

---

## Quick Overview

| **Section** | **Details** |
| :--- | :--- |
| **Business Problem** | Target Brazil needed to understand its e-commerce performance. They didn't have clear answers on order growth, which states drive revenue, where logistics are hurting, and what payment habits reveal. Without this, it's hard to allocate budgets or improve shipping. |
| **Objectives** | 1. Measure growth (yearly, monthly, seasonal trends)<br>2. Spot state-wise patterns (revenue, orders, freight, delivery times)<br>3. Evaluate logistics (delivery accuracy, regional issues)<br>4. Understand payment behavior (credit vs. UPI, installments)<br>5. Provide clear, actionable recommendations |
| **Technical Stack** | SQL (PostgreSQL) – for querying and aggregating data<br>Markdown & PDF – for documentation and sharing insights<br>Presentation – PowerPoint slide deck summarizing key findings |
| **Project Features** | • Analyzed 2 years of real transactional data (2016–2018)<br>• Tracked order growth, seasonality, and time-of-day patterns<br>• Evaluated state performance by customers, revenue, freight, delivery<br>• Measured delivery accuracy (forecast vs. actual)<br>• Analyzed payment method trends and installment usage<br>• Created a summary presentation for stakeholders |
| **Start-to-End Pipeline** | Initial Data Exploration → Growth & Seasonality Analysis → State-wise Performance → Logistics & Delivery Accuracy → Payment Trends → Actionable Recommendations |

---

## The Big Picture

Target expanded into Brazil and wanted to understand how its e-commerce business was performing. Instead of guessing, we dug into two years of real transactional data to uncover what’s working, what’s not, and where we can grow. This repo shares the SQL queries and insights so the Sales, Marketing, and Leadership teams can make smarter decisions.

---

## Business Problem

Target’s Brazil operation needed a clear picture of:

- **How orders are growing** over time.
- **Which states drive revenue** (and which are expensive to serve).
- **Where logistics and delivery** are hurting the customer experience.
- **What payment habits** can tell us about customer preferences.

Without this, it’s hard to allocate marketing budgets, optimize shipping, or improve the checkout experience.

---

## Objectives

- **Measure growth** – yearly, monthly, and seasonal trends.
- **Spot state-wise patterns** – revenue, order volume, freight costs, delivery times.
- **Evaluate logistics performance** – how accurate are delivery estimates? Which regions suffer?
- **Understand payment behavior** – credit vs. UPI, installment usage, shifts over time.
- **Provide actionable recommendations** – not just numbers, but clear next steps.

---
## Repository Structure

    target-brazil-ecommerce-analysis/
    │
    ├── README.md                           
    ├── queries/                            # All SQL scripts
    │   ├── 01_initial_exploration.sql
    │   ├── 02_growth_seasonality.sql
    │   ├── 03_state_performance.sql
    │   ├── 04_logistics_delivery.sql
    │   └── 05_payment_trends.sql
    ├── docs/
    │   └── Target_Brazil_Report.pdf        # The final report
    ├── presentation/                       # PowerPoint slides
    │   └── BUSINESS_CASE_-_TARGET_SQL_PRESENTATION.pptx
    └── visuals/                            # charts from the presentation
        ├── slide_01_cover.png
        ├── slide_02_growth_overview.png
        ├── slide_03_seasonality.png
        ├── slide_04_time_of_day.png
        ├── slide_05_state_revenue.png
        ├── slide_06_freight_cost.png
        ├── slide_07_delivery_time.png
        ├── slide_08_payment_methods.png
        ├── slide_09_installments.png
        └── slide_10_recommendations.png

---
## Technical Stack

- **SQL (PostgreSQL)** – for querying and aggregating the data.
- **Markdown & PDF** – for documentation and sharing.

---

## Dataset Overview

This project uses the **Brazilian E-Commerce Public Dataset** from Kaggle. The dataset contains 8 CSV files covering orders, customers, payments, products, sellers, and more.

### Key Tables Used:

| **Table** | **Description** |
|-------|-------------|
| `customers.csv` | Customer details (IDs, city, state) |
| `geolocation.csv` | ZIP code mapping to lat/long and state |
| `order_items.csv` | Items in each order (price, freight, product/seller IDs) |
| `order_reviews.csv` | Review scores and comments |
| `orders.csv` | Core order data (status, dates, timestamps) |
| `payments.csv` | Payment method, installments, transaction value |
| `products.csv` | Product details (category, dimensions, weight) |
| `sellers.csv` | Seller details (city, state) |

---

# **Analysis Steps**

### 1. Initial Exploration

First, we got to know the data: what fields exist, how many customers, cities, and the date range.

**SQL snippet**
```sql
-- Checking data types and structure
SELECT column_name, data_type 
FROM information_schema.columns 
WHERE table_name = 'customers';

-- Getting time range
SELECT MIN(order_purchase_timestamp), MAX(order_purchase_timestamp)
FROM orders;
```

**Findings:**
- **Orders span** from 2016-09-04 to 2018-10-17 (about 2 years).
- **Customers came from** 4,120 distinct cities across all 27 states – wide coverage.

---

### 2. Growth & Seasonality

We looked at how orders changed year over year and month by month, plus the time of day people prefer to shop.

**SQL snippets**
```sql
-- Yearly growth check
SELECT 
    EXTRACT(YEAR FROM order_purchase_timestamp) AS year,
    COUNT(*) AS order_count
FROM orders
GROUP BY year
ORDER BY year;

-- Monthly seasonality
SELECT 
    EXTRACT(YEAR_MONTH FROM order_purchase_timestamp) AS month,
    COUNT(*) AS order_count
FROM orders
GROUP BY month
ORDER BY month;
```

**Findings:**
- **Orders exploded** from 329 in 2016 → 45,000 in 2017 → 54,000 in 2018.
- **Peaks** in November 2017 (7,544 orders) and January 2018 (7,269 orders).
- **Afternoon (38,361)** and **Night (34,100)** together account for ~73% of all orders. Dawn is quiet.

---

### 3. State-wise Performance

We deep dived into which states contribute the most customers, revenue, and how freight and delivery times vary.

**SQL snippets**
```sql
-- Pulling Customer distribution by state
SELECT 
    customer_state,
    COUNT(DISTINCT customer_id) AS customer_count
FROM customers
GROUP BY customer_state
ORDER BY customer_count DESC;

-- Total and average order price by state
SELECT 
    c.customer_state,
    SUM(oi.price) AS total_revenue,
    AVG(oi.price) AS avg_order_value
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
GROUP BY c.customer_state
ORDER BY total_revenue DESC;

```

**Findings:**
- **SP holds 42% of unique customers** and leads with ~$5.2M in revenue.
- **Northern states like PE, CE, PA** have higher average order values ($145–165) – a premium segment.
- **Freight costs**: SP pays only $15.15 on average; RR and PB pay over $42 – a huge disparity.
- **Delivery times**: SP averages 8.7 days; RR and AP take nearly 30 days.

---

### 4. Logistics & Delivery Accuracy

We compared estimated delivery dates with actual arrivals to see if we’re over-promising.

**SQL snippets**
```sql
-- Delivery time and forecast error
SELECT 
    AVG(DATEDIFF(order_delivered_customer_date, order_purchase_timestamp)) AS actual_delivery_time,
    AVG(DATEDIFF(order_estimated_delivery_date, order_delivered_customer_date)) AS forecast_error
FROM orders
WHERE order_status = 'delivered';

```

**Findings:**
- **Average fulfillment cycle:** 12.09 days.
- **Forecast error:** 10.96 days – meaning customers receive their orders **11 days earlier** than the promised date.
- In **Northern states**, the "expectation gap" is huge (17–20 days early). Great for delight, but we could set tighter estimates to boost conversion.

---

### 5. Payment Trends

We examined how payment methods evolved and how customers use installments.

**SQL snippets**
```sql
-- Monthly orders by payment type
SELECT 
    EXTRACT(YEAR_MONTH FROM o.order_purchase_timestamp) AS month,
    p.payment_type,
    COUNT(*) AS order_count
FROM orders o
JOIN payments p ON o.order_id = p.order_id
GROUP BY month, p.payment_type
ORDER BY month, p.payment_type;

-- Installment usage
SELECT 
    payment_installments,
    COUNT(*) AS order_count,
    AVG(payment_value) AS avg_payment
FROM payments
GROUP BY payment_installments
ORDER BY payment_installments;
```

**Findings:**
- **Credit cards dominate (~75%)** and grew from 254 orders (Oct 2016) to 4,900 (Aug 2018).
- **UPI share slipped** from 20% to 17%.
- **Debit cards jumped** from 0.71% to 4.14% in mid-2018 – worth investigating.
- **Vouchers became nearly 100%** of payments in the last two months of data.
- **52% of orders** are paid in full; **31.6%** use 2–4 installments; a small group uses 10+ installments for big-ticket items.

---
# Top Actionable Insights & Recommendations


## Key Insights

- **Growth is strong**, especially in 2017 and 2018.
        <img width="2000" height="1123" alt="image" src="https://github.com/user-attachments/assets/f66ba9e7-b1cd-4de9-b7b4-8af470b6b16f" />
        
- **Customer Behavior -Seasonal & Daily Patterns Analysis**
      <img width="2000" height="1125" alt="image" src="https://github.com/user-attachments/assets/8bea7b92-d24f-4950-9309-09724444efcb" />
    - Strong Seasonal Peaks in Late Spring & Summer
        - *Insight:* Order volumes surge during November–March, with peaks in November 2017 (7,544 orders), January 2018 (7,269 orders), and March 2018 (7,211 orders).
        - *Business Action:* Pre-stock warehouses by October to avoid stockouts during these high-demand months.
    - Afternoon & Night Dominate Order Volume
        - *Insight:* Afternoon (38,361) and Night (34,100) together account for ~73% of all orders. Dawn hours see very minimal activity.
        - *Business Action:* Use morning-only discounts to shift some demand to earlier hours, balancing warehouse workload and delivery capacity.
    - Clear Seasonal & Daily Patterns Exist
        - *Insight:* Both seasonal and time-of-day patterns are consistent and predictable, allowing for data-driven planning.
        - *Business Action:* Align marketing campaigns, inventory planning, and staffing with these peak periods for maximum efficiency.
     
        **Quick Summary**
      
        | **Pattern** | **Key Finding** | **Actionable Insight** |
        | :--- | :--- | :--- |
        | **Seasonal** | Peaks in Nov, Jan, Mar | Stock up by October |
        | **Time of Day** | Afternoon + Night = 73% of orders | Morning discounts to shift demand |
        | **Consistency** | Predictable patterns | Plan marketing & operations accordingly |


- **SP is the engine**, but Northern states have **higher-value customers** (and much higher logistics cost).
- **Freight costs and delivery times vary wildly** – the North/Northeast need attention.
      <img width="1253" height="725" alt="image" src="https://github.com/user-attachments/assets/5d2ec066-d707-42c1-a3c7-ee40df17dfe7" />
      <img width="1098" height="472" alt="image" src="https://github.com/user-attachments/assets/0c6e7450-a2d7-40a9-a447-8dfeca8a7309" />

     
- **We deliver earlier than promised** (by ~11 days) – this is Valuable
      <img width="1217" height="310" alt="image" src="https://github.com/user-attachments/assets/6b786d9d-3db6-4afb-8cd8-9deae5577507" />
        <img width="455" height="487" alt="image" src="https://github.com/user-attachments/assets/05bf774b-7952-4d1d-9d39-a017136b45e5" />



- **Credit card rules**, but alternative payments (UPI, debit, vouchers) are showing shifts.
      <img width="1072" height="640" alt="image" src="https://github.com/user-attachments/assets/4f95e134-dd8b-491d-b841-68e22abf3243" />
      <img width="1266" height="127" alt="image" src="https://github.com/user-attachments/assets/29a4e096-b4f9-4223-8e97-0404735108db" />
      <img width="511" height="572" alt="image" src="https://github.com/user-attachments/assets/5599b242-a131-4ec3-9b9c-f409d2ba0317" />




---

## **Top Strategic Recommendations**

### 1. Focus on High-Potential States

Since **42% of our high-value customers are in SP**, we should prioritize rolling out new features, faster delivery, and loyalty rewards in this region. Although these states have fewer customers, they spend much more per order ($150+). Focus on selling premium products in these areas to maximize revenue.

### 2. Optimize Logistics for Remote States

Opening a small warehouse in the Northeast could significantly cut the current $42 average shipping cost. Experiment with free shipping on expensive orders in the Northeast. This encourages customers to buy more at once, making the high travel costs worth it for the company.

### 3. Capitalize on Seasonal Peaks

Sales spike from November through March. We should stock up main warehouses by October so we don't run out of inventory during these peak months. Most people shop in the afternoon and evening. Offering "Morning-Only" discounts can shift some traffic to earlier hours, helping the warehouse team manage the daily workload more effectively.

### 4. Promote Alternative Payment Methods

Credit card processing fees reduce company profits. Offering a small **2-3% discount** for using UPI or Debit cards can help protect our margins. Many customers prefer 10-month payment plans for expensive items. Promoting high-end electronics or furniture with free installation can help these customers decide to buy.

### 5. Monitor and Improve Delivery Performance

We currently deliver **11 days earlier than promised**. Updating our checkout to show these faster, more accurate arrival dates will lead to significantly higher sales. It takes nearly a month to reach states like RR. Partnering with local delivery companies in these spots can cut wait times, keep customers happy, and reduce long-term churn.

### 6. Leverage Customer Reviews

Use "Arrived 10 days early!" stories in advertisements. This builds immediate trust with new shoppers. For customers in far-away states, send a "We're almost there" message halfway through the delivery process. This proactive communication makes the long wait feel much shorter.

---

## How to Use This Repository

1. **Clone the repo:**
   ```bash
   git clone https://github.com/your-username/target-brazil-ecommerce-analysis.git
   ```

2. **Load the data** into your SQL environment (the dataset is not included here due to size; contact the team if needed).

3. **Run the SQL queries** in the `queries/` folder (or copy from the snippets above) to reproduce the analysis.

4. **Explore** – tweak the queries to ask your own questions.

---

## How to Run

1. Clone the repository.
2. Import the provided dataset into your SQL environment.
3. Run the queries in the `queries/` folder in the suggested order.
4. Review the output to reproduce the insights.

---
## 👤 Author

### Shaik Mayeenuddin

#### Business Analyst | Data Analytics & AI/ML | Optimizing Processes to Drive Revenue & Retention

🔗https://www.linkedin.com/in/shaikmayeenuddin

