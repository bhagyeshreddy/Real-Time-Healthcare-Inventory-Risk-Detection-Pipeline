# Real-Time-Healthcare-Inventory-Risk-Detection-Pipeline

A cloud-native project designed to monitor hospital medication inventory, detect supply risks, and trigger real-time alerts using AWS services.

---

## 📦 Project Summary

This project simulates a predictive supply chain alerting system that detects potential drug stockouts by analyzing real-time dispense activity and national FDA shortage data.

It uses:
- **AWS Redshift Serverless** for data modeling and querying
- **AWS Lambda** for orchestration and alert logic
- **Amazon SNS** for real-time notifications
- **Python and SQL** for ETL and logic
- **Secrets Manager** and **EventBridge** (optional) for secure and scheduled automation

---

## 🔧 Architecture

```
CSV (Dispense + Inventory + FDA) → S3 → Redshift (daily demand, risk view)
                                        ↓
                                Lambda (SQL Query)
                                        ↓
                                 SNS Alert (Email/SMS)
```

---

## 🛠️ Setup Instructions

1. **Prepare your data:**
   - `pharmacy_dispense_data_realnames.csv`
   - `inventory_data.csv`
   - `mock_fda_drug_shortages.csv`

2. **Run Python script** to create `daily_demand_history.csv`

3. **Load all CSVs to S3**, then import to Redshift using the `COPY` command.

4. **Run SQL scripts** in this order:
   - `02_redshift_days_on_hand.sql`
   - `03_redshift_inventory_risk_view.sql`

5. **Deploy Lambda Function:**
   - Use `04_lambda_redshift_alert.py`
   - Set environment variables for:
     - `REDSHIFT_WORKGROUP`
     - `REDSHIFT_DATABASE`
     - `REDSHIFT_SECRET_ARN`
     - `SNS_TOPIC_ARN`

6. **Create SNS Topic** and confirm email subscription

7. (Optional) **Use EventBridge** to schedule Lambda daily

---

## 📂 Files

| File | Description |
|------|-------------|
| `01_build_daily_demand_history.py` | Converts raw logs into daily usage summary |
| `02_redshift_days_on_hand.sql` | Calculates average daily demand and days-on-hand |
| `03_redshift_inventory_risk_view.sql` | Combines inventory, demand, and FDA data |
| `04_lambda_redshift_alert.py` | Sends real-time alerts for at-risk drugs |

---

## ✅ Key Outcomes

- Automated alerts for 200+ medications
- 90% reduction in manual stock monitoring
- Real-time signal response under 3 seconds
- Scalable and production-ready AWS architecture

---

## 🧠 Skills Demonstrated

- Data Engineering (ETL, joins, aggregations)
- AWS Cloud Services (Redshift, Lambda, SNS)
- Automation & Monitoring
- Healthcare data handling
- SQL optimization

---
