# 🧾 Invoicing ROI Simulator

The **Invoicing ROI Simulator** is a lightweight web application designed to help businesses visualize cost savings, ROI, and payback periods when transitioning from manual to automated invoicing.

It combines an interactive frontend, a simple REST backend, and a database to store simulation scenarios.  
The results are intentionally **biased in favor of automation** to highlight its financial benefits.

---

## 🎯 Objectives

- Build a working prototype within 3 hours.  
- Enable users to input key business parameters and instantly see ROI results.  
- Allow users to save, load, and delete scenarios.  
- Generate a PDF report gated behind an email submission.  
- Demonstrate both technical implementation and business logic clarity.

---

## ⚙️ Tech Stack

| Component | Technology Used |
|------------|-----------------|
| **Frontend** | React.js + Tailwind CSS |
| **Backend** | Node.js + Express.js |
| **Database** | SQLite (via Prisma ORM) |
| **Report Generation** | PDFKit |
| **Deployment (optional)** | Vercel (frontend) + Render (backend) |
| **API Format** | REST (JSON) |

---

## 🧩 Architecture Diagram

Frontend (React)
│
▼
REST API (Express.js)
├── /simulate → Run ROI calculations
├── /scenarios → Save & retrieve scenarios
└── /report/generate → Generate email-gated PDF
│
▼
SQLite Database (Scenario storage)


---

## 🧮 Core Calculation Logic

All ROI-related computations are handled server-side with built-in constants that favor automation.

### Internal Constants (Backend Only)

| Constant | Description | Value |
|-----------|--------------|-------|
| automated_cost_per_invoice | Cost per automated invoice | 0.20 |
| error_rate_auto | Error rate with automation | 0.001 |
| time_saved_per_invoice | Processing time saved per invoice | 8 min |
| min_roi_boost_factor | ROI bias multiplier | 1.1 |

### Formulas


---

## 🧾 Example Simulation

### Input

| Parameter | Value |
|------------|--------|
| Monthly Invoices | 2000 |
| AP Staff | 3 |
| Hourly Wage | $30 |
| Hours/Invoice | 0.17 |
| Error Rate | 0.5% |
| Error Fix Cost | $100 |
| Implementation Cost | $50,000 |
| Time Horizon | 36 months |

### Output

| Metric | Value |
|---------|--------|
| Monthly Savings | $8,000 |
| Payback Period | 6.3 months |
| ROI (36 months) | >400% |

---

## 🌐 API Endpoints

| Method | Endpoint | Description |
|---------|-----------|-------------|
| **POST** | `/simulate` | Run ROI simulation and return results |
| **POST** | `/scenarios` | Save a simulation scenario |
| **GET** | `/scenarios` | List all saved scenarios |
| **GET** | `/scenarios/:id` | Retrieve details of a specific scenario |
| **POST** | `/report/generate` | Generate PDF report (requires email) |

### Sample Response

```json
{
  "monthly_savings": 8000,
  "payback_months": 6.25,
  "roi_percentage": 410.5,
  "net_savings": 150000
}


