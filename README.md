# Supply-Chain-Fuel-Variance-Analysis
Creating a model that detects any anomalies in fleet trucks using predictive models

# N3 Corridor Logistics Intelligence & Fuel Variance Analytics

## Project Overview
Supply chain operators along the critical Durban-to-Johannesburg **N3 corridor** face severe profit leakage due to hidden fuel variance and excessive idle times. This project delivers an end-to-end data analytics and predictive modeling pipeline designed to expose operational inefficiencies, isolate rogue assets, and protect bottom-line margins.

## Tech Stack
* **Language:** Python
* **Data Manipulation & Analysis:** Pandas, NumPy
* **Machine Learning:** Scikit-learn (Random Forest Classifier)
* **Environment:** Jupyter Notebook / Anaconda
* **Visualization:** Matplotlib, Seaborn

## Key Features & Methodology
**1. Synthetic Telemetry & "Trojan Horse" Injection**

Generated a realistic, 50,000-record fleet logistics dataset simulating multi-leg trips along the N3 route.

Programmatically injected controlled anomalies ("Trojan Horses"), forcing specific rogue trucks (e.g., TRK-012, TRK-033) to consistently burn ~21% more fuel than baseline expectations, and specific loading docks to exhibit heavy idle-time penalties.

**2. Exploratory Data Analysis (EDA)**

Analyzed descriptive statistics across expected vs. actual fuel consumption.

Mapped variance percentages across route legs using Seaborn distribution plots to isolate choke points.

**3. Predictive Modeling (Machine Learning)**

Trained a Random Forest Classifier using Scikit-learn to predict the probability of a trip resulting in a high-variance fuel anomaly based on expected fuel consumption and idle time.

Achieved ~94% model accuracy in identifying operational risk factors before trips are even completed.

## Next Steps
Phase 1 Extension: Power BI Executive Dashboard integration (Star Schema modeling and CFO-level DAX measures in ZAR).

Automation: Real-time alert workflows via n8n and Microsoft Teams for human-in-the-loop exception handling.
