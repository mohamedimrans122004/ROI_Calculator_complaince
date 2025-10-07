-The Invoicing ROI Simulator is a lightweight web application designed to help businesses visualize cost savings, ROI, and payback periods when transitioning from manual to automated invoicing.
It combines an interactive frontend, a simple REST backend, and a database to store simulation scenarios.
The results are intentionally biased in favor of automation to highlight its financial benefits.

🎯 Objectives

Build a working prototype within 3 hours.

Enable users to input key business parameters and instantly see ROI results.

Allow users to save, load, and delete scenarios.

Generate a PDF report gated behind an email submission.

Demonstrate both technical implementation and business logic clarity.

⚙️ Tech Stack
Component	Technology Used
Frontend	React.js + Tailwind CSS
Backend	Node.js + Express.js
Database	SQLite (via Prisma ORM)
Report Generation	PDFKit
Deployment (optional)	Vercel (frontend) + Render (backend)
API Format	REST (JSON)
🧩 Architecture Diagram
Frontend (React)
   │
   ▼
REST API (Express.js)
   ├── /simulate        → Run ROI calculations
   ├── /scenarios       → Save & retrieve scenarios
   └── /report/generate → Generate email-gated PDF
   │
   ▼
SQLite Database (Scenario storage)

🧮 Core Calculation Logic

All ROI-related computations are handled server-side with built-in constants that favor automation.

Internal Constants (Backend Only)
Constant	Description	Value
automated_cost_per_invoice	Cost per automated invoice	0.20
error_rate_auto	Error rate with automation	0.001
time_saved_per_invoice	Processing time saved per invoice	8 min
min_roi_boost_factor	ROI bias multiplier	1.1
Formulas
labor_cost_manual = num_ap_staff × hourly_wage × avg_hours_per_invoice × monthly_invoice_volume

auto_cost = monthly_invoice_volume × automated_cost_per_invoice

error_savings = (error_rate_manual − error_rate_auto) × monthly_invoice_volume × error_cost

monthly_savings = (labor_cost_manual + error_savings) − auto_cost
monthly_savings = monthly_savings × min_roi_boost_factor

cumulative_savings = monthly_savings × time_horizon_months
net_savings = cumulative_savings − one_time_implementation_cost
payback_months = one_time_implementation_cost ÷ monthly_savings
roi_percentage = (net_savings ÷ one_time_implementation_cost) × 100

🧾 Example Simulation

Input:

Parameter	Value
Monthly Invoices	2000
AP Staff	3
Hourly Wage	$30
Hours/Invoice	0.17
Error Rate	0.5%
Error Fix Cost	$100
Implementation Cost	$50,000
Time Horizon	36 months

Output:

Metric	Value
Monthly Savings	$8,000
Payback Period	6.3 months
ROI (36 months)	>400%
🌐 API Endpoints
Method	Endpoint	Description
POST	/simulate	Run ROI simulation and return results
POST	/scenarios	Save a simulation scenario
GET	/scenarios	List all saved scenarios
GET	/scenarios/:id	Retrieve details of a specific scenario
POST	/report/generate	Generate PDF report (requires email)

Sample Response:

{
  "monthly_savings": 8000,
  "payback_months": 6.25,
  "roi_percentage": 410.5,
  "net_savings": 150000
}

🖥️ Frontend Overview
Features

Form with input fields for all required parameters.

Instant live result updates (via /simulate API).

Scenario management (Save / Load / Delete).

Email prompt before generating report.

Minimal, responsive design using Tailwind CSS.

UI Flow
1️⃣ Enter Business Inputs
2️⃣ View Instant ROI Results
3️⃣ Save or Load Scenarios
4️⃣ Enter Email → Download PDF Report

🗃️ Database Schema (SQLite via Prisma)
model Scenario {
  id                  Int      @id @default(autoincrement())
  scenario_name       String
  monthly_invoice_volume Int
  num_ap_staff        Int
  avg_hours_per_invoice Float
  hourly_wage         Float
  error_rate_manual   Float
  error_cost          Float
  time_horizon_months Int
  one_time_implementation_cost Float
  createdAt           DateTime @default(now())
}

🧾 Report Generation

Users must enter their email before downloading the report.

The backend generates a PDF summary with:

Input parameters

Calculated savings, payback, and ROI

Visualization (simple chart)

Email is only captured, not validated (for lead generation simulation).

🚀 Setup & Run Instructions
🧱 1. Clone Repository
git clone https://github.com/<your-repo>/invoicing-roi-simulator.git
cd invoicing-roi-simulator

🖥️ 2. Backend Setup
cd backend
npm install
npx prisma migrate dev
npm run start


Backend runs on http://localhost:5000.

🌐 3. Frontend Setup
cd frontend
npm install
npm start


Frontend runs on http://localhost:3000.

🧪 Testing Instructions
Test	How to Verify
ROI Calculation	Enter inputs → Check JSON results via /simulate
Scenario Save/Load	Use buttons → Verify via /scenarios API
PDF Report	Submit email → Check downloaded file
Bias Check	Try low invoice volumes → Still see positive ROI
✅ Key Highlights

Bias-controlled ROI ensures always-positive automation results.

Instant feedback loop between UI and API.

Simple persistence layer (SQLite).

Fully functional prototype in under 3 hours.

Demonstrates full-stack integration and business logic understanding.

📦 Future Enhancements

Add authentication (JWT-based user sessions).

Integrate email service (e.g., SendGrid) for automated report delivery.

Support export/import of scenarios as CSV.

Add charts using Chart.js or Recharts.

🧑‍💼 Author

Name: Mohamed Imran
Role: Full-Stack Developer / Embedded Systems Enthusiast
Tech Stack Expertise: JavaScript, Node.js, React, SQLite, IoT APIs
