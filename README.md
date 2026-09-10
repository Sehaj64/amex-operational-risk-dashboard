# 🏦 American Express GMNS | Enterprise Operational Risk & Regulatory Issues Intelligence Dashboard

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](Enterprise_Operational_Risk_Dashboard.pbix)
[![DAX](https://img.shields.io/badge/DAX-Calculated_Measures-002663?style=for-the-badge)](README.md)
[![Live Web App](https://img.shields.io/badge/Live_Web_App-Interactive-0284c7?style=for-the-badge)](index.html)
[![Dataset](https://img.shields.io/badge/Dataset-CFPB_Federal_Log-059669?style=for-the-badge)](https://www.consumerfinance.gov/)

An enterprise-grade **Operational Risk, Issues Governance, and SLA Analytics Dashboard** tailored specifically to the **American Express Global Merchant & Network Services (GMNS) - Global Governance, Risk, Remediation & Operations (GRRO)** team.

---

## 🚀 Live Interactive Access & Downloads

- 📥 **[Download Working Power BI File (.pbix)](Enterprise_Operational_Risk_Dashboard.pbix)**
- 🌐 **[Interactive Web Version (Open index.html)](index.html)**

---

## 🎯 Executive Summary & Business Context

In enterprise payment networks and merchant acquiring, operational breakdowns—such as settlement clearing batch delays, partner acquirer API timeouts, merchant onboarding KYC bottlenecks, and disputed chargeback queues—create direct regulatory scrutiny and operational loss exposure.

This project ingests **62,516 real-world banking and payment records** from the U.S. Consumer Financial Protection Bureau (CFPB) regulatory database, transforming complex operational records into self-service C-Suite Key Risk Indicators (KRIs), root cause thematic analysis, and geographic remediation tracking.

---

## 📊 Core Key Risk Indicators (KRIs)

| Key Risk Indicator | Filtered Value | Target SLA | Business Meaning |
| :--- | :---: | :---: | :--- |
| **Total Filtered Issues** | **3,000** | — | Total operational friction volume in selected business segment |
| **SLA Timeliness Breaches** | **173** | 0 | Cases exceeding mandated regulatory response timeframe |
| **SLA Breach Rate %** | **6.88%** | **< 5.00%** | Key risk compliance threshold metric (breach alert) |
| **Monetary Customer Remediation** | **100** | Minimize | Cases requiring direct monetary compensation / financial loss |

---

## 🛠️ Production DAX Measure Library

### 1. Total Issues
```dax
Total Issues = COUNTROWS('Real_CFPB_Consumer_Complaints')
```

### 2. SLA Timeliness Breaches (Untimely Responses)
```dax
SLA Breaches = 
CALCULATE(
    COUNTROWS('Real_CFPB_Consumer_Complaints'), 
    'Real_CFPB_Consumer_Complaints'[Timely response?] = "No"
)
```

### 3. SLA Breach Rate %
```dax
SLA Breach Rate % = 
DIVIDE([SLA Breaches], [Total Issues], 0)
```

### 4. Monetary Remediation Count (Direct Customer Loss Compensation)
```dax
Monetary Remediation Count = 
CALCULATE(
    COUNTROWS('Real_CFPB_Consumer_Complaints'), 
    'Real_CFPB_Consumer_Complaints'[Company response to consumer] = "Closed with monetary relief"
)
```

---

## 🔍 Key Risk Insights & Root Cause Investigations

### 1. Pareto Root Cause Concentration (The 80/20 Rule)
- In the Debt Collection & Disputed Settlement portfolio, **"Attempts to collect debt not owed"** constitutes **1,218 issues (over 50% of the entire portfolio)**.
- Second highest driver: **"Written notification about debt"** with **459 issues**.
- **Actionable Insight**: Automating the pre-collection validation pipeline directly mitigates >60% of all customer escalations.

### 2. Digital Channel Vulnerability
- **89.26%** of all complaints originate through **Web Portals**, demonstrating that digital UI latency and self-service exceptions drive the majority of consumer dissatisfaction.

### 3. Geographic Resolution & Settlement Hotspots
- **California** (338 closed with explanation, 23 monetary relief) and **Florida** (250 closed with explanation, 11 monetary relief) represent the highest density of financial remediation exposure.

---

## 📂 Repository File Structure

```
amex-operational-risk-dashboard/
├── Enterprise_Operational_Risk_Dashboard.pbix   # Primary Power BI Desktop file (Data model + visuals)
├── index.html                                   # Self-contained, interactive web dashboard replica
└── README.md                                    # Executive report, DAX dictionary & documentation
```

---

## 💼 Role Alignment: American Express GMNS Risk Reporting & Analytics

This dashboard directly fulfills every key competency required in the American Express GMNS Risk Analyst specification:
- **Issues, OREs & Remediation Analytics**: Quantifies operational issues and remediation velocity.
- **Root Cause & Trend Investigations**: Leverages Pareto sorting to isolate high-risk drivers.
- **Executive-Ready Storytelling**: Formatted for C-Suite risk committees and regulatory compliance oversight.
- **Self-Service Analytics**: Dynamic interactive slicing across products, states, and SLA adherence flags.

---

*Author: Sehaj Kumar | Operational Risk & Analytics Portfolio*
