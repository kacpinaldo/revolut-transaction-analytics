HEAD
# Revolut Transaction Analytics (Simulated Data Project) 💳

**Goal:** Analyze simulated Revolut-style transaction data using SQL and Python to identify user behavior patterns and detect anomalies in spending.

---

## 📊 Project Overview

This project simulates a dataset of financial transactions inspired by Revolut’s data analytics workflows.  
The main goals were to:
- Generate realistic synthetic transaction data (user_id, amount, country, category, payment method, status, timestamp)  
- Store and query data using **SQLite + SQL**  
- Identify spending anomalies and transaction irregularities  
- Visualize aggregated results in **Python (Pandas + Matplotlib)**  

> ⚠️ All data in this project is **fully synthetic**, created using Python’s `faker` library for educational and portfolio purposes only.

---

## 🧠 SQL Analysis

Key SQL tasks include:
- **Aggregations:** total and average spending by merchant, country, and category  
- **Filtering:** analyzing Completed vs Failed transactions  
- **Window functions:** ranking top categories per country  
- **CTEs:** for organizing multi-step analytical queries  
- **Anomaly detection:** users with transactions exceeding 3× their own average  
- **Sequential logic:** users with more than 3 consecutive failed transactions  

Example query:

```sql
WITH avg_amount AS (
  SELECT user_id, AVG(amount) AS avg_user_amount
  FROM transactions
  WHERE transaction_status = 'Completed'
  GROUP BY user_id
)
SELECT t.user_id, t.amount, s.avg_user_amount
FROM transactions AS t
JOIN avg_amount AS s USING (user_id)
WHERE t.transaction_status = 'Completed'
  AND t.amount > 3 * s.avg_user_amount;



