# Target Brazil – E‑commerce Analysis

---




## Quick Section Summary

- Why this Project
- Business Problem
- Objectives
- Technical Stack
- Repository Structure

---

## Why This Project

Target expanded into Brazil and wanted to understand how its e‑commerce business was performing. Instead of guessing, we dug into two years of real transactional data to uncover what’s working, what’s not, and where we can grow. This repo shares the SQL queries and insights so the Sales, Marketting teams and Leadership team can make smarter decisions.

---

## Business Problem

Target’s Brazil operation needed a clear picture of:

- How orders are growing over time.
- Which states drive revenue (and which are expensive to serve).
- Where logistics and delivery are hurting the customer experience.
- What payment habits can tell us about customer preferences.

Without this, it’s hard to allocate marketing budgets, optimize shipping, or improve the checkout experience.

---

## Objectives

1. **Measure growth** – yearly, monthly, and seasonal trends.
2. **Spot state‑wise patterns** – revenue, order volume, freight costs, delivery times.
3. **Evaluate logistics performance** – how accurate are delivery estimates? Which regions suffer?
4. **Understand payment behavior** – credit vs. UPI, installment usage, shifts over time.
5. **Provide actionable recommendations** – not just numbers, but clear next steps.

---

## Technical Stack

- **SQL** (PostgreSQL / MySQL) – for querying and aggregating the data.

- **Markdown & PDF** – for documentation and sharing.

---

## Repository Structure
target-brazil-ecommerce-analysis/
│
├── README.md # You’re here
├── queries/ # All SQL scripts (optional, if you separate files)
│ ├── 01_initial_exploration.sql
│ ├── 02_growth_seasonality.sql
│ └── ...
├── docs/
│ └── Target_Brazil_Report.pdf # The final printed report
└── visuals/ # Any charts or images (optional)
└── order_trends.png


## Analysis Steps

### 1. Initial Exploration

First, we got to know the data: what fields exist, how many customers, cities, and the date range.

** SQL snippet**  
*(Paste your SQL code snapshot here – e.g., query to check distinct cities/states)*

**Findings:**  
- Orders span from **2016‑09‑04 to 2018‑10‑17** (about two years).  
- Customers came from **4120 distinct cities** across all 27 states – wide coverage.

---

### 2. Growth & Seasonality

We looked at how orders changed year over year and month by month, plus the time of day people prefer to shop.

** SQL snippets**  
*(Paste your yearly order count, monthly order count, and time‑of‑day queries here)*

**Findings:**  
- Orders exploded from **329 in 2016** → **45,000 in 2017** → **54,000 in 2018**.  
- Peaks in **November 2017** (7,544 orders) and **January 2018** (7,269 orders).  
- **Afternoon (38,361)** and **Night (34,100)** together account for ~73% of all orders. Dawn is quiet.

---

### 3. State‑wise Performance

We drilled into which states contribute the most customers, revenue, and how freight and delivery times vary.

** SQL snippets**  
*(Paste queries for: customer distribution by state, total/average order price per state, freight value per state)*

**Findings:**  
- **SP** holds **42%** of unique customers and leads with ~$ 5.2M in revenue.  
- Northern states like **PE, CE, PA** have higher average order values ($ 145–165) – a premium segment.  
- Freight costs: **SP** pays only **$ 15.15** on average; **RR** and **PB** pay over **$ 42** – a huge disparity.  
- Delivery times: **SP** averages **8.7 days**; **RR** and **AP** take nearly **30 days**.

---

### 4. Logistics & Delivery Accuracy

We compared estimated delivery dates with actual arrivals to see if we’re over‑promising.

** SQL snippets**  
*(Paste query for delivery time difference and forecast error)*

**Findings:**  
- Average fulfillment cycle: **12.09 days**.  
- Forecast error: **10.96 days** – meaning customers receive their orders **11 days earlier** than the promised date.  
- In Northern states, the “expectation gap” is huge (17–20 days early). Great for delight, but we could set tighter estimates to boost conversion.

---

### 5. Payment Trends

We examined how payment methods evolved and how customers use installments.

** SQL snippets**  
*(Paste queries for monthly orders by payment type and installment distribution)*

**Findings:**  
- **Credit cards** dominate (~75%) and grew from 254 orders (Oct 2016) to 4,900 (Aug 2018).  
- **UPI** share slipped from 20% to 17%.  
- **Debit cards** jumped from 0.71% to 4.14% in mid‑2018 – worth investigating.  
- **Vouchers** became nearly 100% of payments in the last two months of data.  
- **52%** of orders are paid in full; **31.6%** use 2–4 installments; a small group uses 10+ installments for big‑ticket items.

---

## Key Insights (Quick Summary)

- **Growth is strong**, especially in 2017 and 2018.  
- **SP is the engine**, but Northern states have higher‑value customers (and much higher logistics cost).  
- **We deliver earlier than promised** (by ~11 days) – this is a hidden asset.  
- **Freight costs and delivery times vary wildly** – the North/Northeast need attention.  
- **Credit card rules**, but alternative payments (UPI, debit, vouchers) are showing shifts.

---

## Recommendations

1. **Double down on SP** – faster delivery, loyalty perks, new features.  
2. **Help Northern states** – open a small warehouse in the Northeast to cut freight costs; try free shipping on high‑value orders.  
3. **Prepare for seasonal spikes** – stock up by October; use morning discounts to spread workload.  
4. **Encourage lower‑cost payments** – give 2–3% discounts for UPI/debit to save on credit card fees.  
5. **Update delivery estimates** – show the real 12‑day average at checkout; it builds trust.  
6. **Use “early delivery” in marketing** – stories of “arrived 10 days early” make new shoppers confident.

---

## How to Use This Repository

1. **Clone** the repo:  
   `git clone https://github.com/your-username/target-brazil-ecommerce-analysis.git`
2. **Load the data** into your SQL environment (the dataset is not included here due to size; contact the team if needed).
3. **Run the SQL queries** in the `queries/` folder (or copy from the snippets above) to reproduce the analysis.
4. **Explore** – tweak the queries to ask your own questions.

---





## How to Run
- Clone the repository.
- Import the provided dataset into your SQL environment.
- Run the queries in the queries/ folder in the suggested order.
- Review the output to reproduce the insights.





## Author
Shaik Mayeenuddin
Aspiring Data Scientist Professional | Supply Chain & Marketing Analytics Expert Pursuing a Master’s in Data Science (AI & ML) Student 🔗 https://www.linkedin.com/in/shaikmayeenuddin

