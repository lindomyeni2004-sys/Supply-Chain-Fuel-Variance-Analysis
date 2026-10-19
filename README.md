# Supply-Chain-Fuel-Variance-Analysis
Creating a model that detects any anomalies in fleet trucks using predictive models

# N3 Corridor Logistics Intelligence & Fuel Variance Analytics

## Project Overview

Supply chain operators along the critical Durban-to-Johannesburg **N3 corridor** face severe profit leakage due to hidden fuel variance and excessive idle times. This project delivers an end-to-end data analytics and predictive modeling pipeline designed to expose operational inefficiencies, isolate rogue assets, and protect bottom-line margins.

## Tech Stack

| **Data Engine & ML** | Python, Pandas, NumPy, Scikit-learn | Synthetic telemetry generation, anomaly injection, classification |
| **Business Intelligence** | Power BI Desktop, DAX, Power Query | Star Schema dimensional modeling, financial variance metrics (ZAR) |
| **Workflow Automation** | n8n (Self-Hosted), REST APIs, Webhooks | Event-driven orchestration, in-flight JavaScript calculation |
| **Communications** | Google Cloud Console, Gmail OAuth2 API | Automated, authenticated HTML incident dispatching |


## Pipeline Breakdown

### Layer 1: Data Engineering & Predictive ML (Python)
**Synthetic Corridor Simulation:** Modeled 50,000 multi-leg freight trips incorporating realistic transit physics, elevation choke points (Cato Ridge, Town Hill, Van Reenen's Pass), and distribution depot waypoints (City Deep).
**Controlled Anomaly Injection:** Programmatically introduced discrete operational failures—including mechanical fuel injector failure and off-route fuel siphonage (+21% burn rate) along with chronic dock loading bottlenecks.
**Predictive Classification:** Engineered a Scikit-learn **Random Forest Classifier** trained on trip baselines, expected consumption, and stage dwell times. Achieved **94% model accuracy** in identifying high-risk trip profiles prior to destination arrival.

### Layer 2: CFO-Grade Analytics & Dimensional Modeling (Power BI)
**Star Schema Architecture:** Separated high-volume transactional logs (`Fact_Trips`) from dimensional attributes (`Dim_Truck`, `Dim_Driver`) to ensure high-performance query execution and clean filter context.
**Financial DAX Modeling (ZAR):**
* **Fuel Variance Cost:** Evaluated against a fleet baseline of **R23.50 / Liter**.
* **Operational Holding Cost:** Factored at **R350.00 / Hour**. This metric holistically accounts for driver wages, asset lease amortization, insurance overhead, and opportunity costs from missed return loads.
**Executive Findings:**
* **R1,430,000+** lost to unbudgeted fuel variance.
* **R12,370,000+** lost to non-productive idle delays.
* **Outlier Isolation:** Scatter plot analysis separated driver behavior from fleet mechanics, isolating **5 rogue trucks** (`TRK-012`, `TRK-033`, `TRK-045`, `TRK-078`, `TRK-089`) showing consistent +21% excess burn across varying operators.

### Layer 3: Event-Driven Automation & Escalation (n8n)
**Webhook Endpoint:** An event-driven listener captures real-time telemetry payloads as vehicles log leg checkpoints.
**In-Flight Logic:** An internal JavaScript Code node parses the payload, executes the financial cost equations in real time, and evaluates dynamic risk thresholds
**Closed-Loop Escalation:** High-risk payloads route through an **If-node** to generate structured, CFO-grade HTML incident cards, instantly emailed to dispatch supervisors via authenticated **Google Cloud OAuth2**.
**Verified Test Case:** Asset `TRK-012` caught on the Cato Ridge to Pietermaritzburg leg (+35.7% variance, 4.0 hrs idle) $\rightarrow$ **R2,575.00 immediate margin loss** flagged and dispatched in seconds.

## Quickstart & Execution
### 1. Python Environment Setup
- Clone the repository
- Install dependencies: VS Code or Jupyter Notebook through Anaconda
- Run simulation & train model

### 2. Power BI Dashboard
- Open Fuel_Variance_Analytics.pbix in Power BI Desktop.
- Refresh data source paths if referencing local .xls outputs.

### 3. n8n Incident Automation
- Launch your local n8n instance
- In the n8n UI, import N3 Fleet Incident Escalation.json.
- Connect your Google Cloud OAuth2 credentials for Gmail.
- Test the pipeline via PowerShell:
Invoke-RestMethod -Uri "<Webhook-URL>" -Method Post -ContentType "application/json" -Body '{"trip_id":"TRP-98421","truck_id":"TRK-012","driver_name":"Sipho Khumalo","route_leg":"Cato Ridge to Pietermaritzburg","expected_fuel_liters":140.0,"actual_fuel_liters":190.0,"variance_percent":35.7,"idle_time_mins":240,"requires_escalation":true}'
