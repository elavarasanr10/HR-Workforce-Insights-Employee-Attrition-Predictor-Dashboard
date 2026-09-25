# HR Workforce Insights & Employee Attrition Predictor Dashboard

A Power BI dashboard that tracks workforce composition and flags employees at risk of leaving — built to mirror how an HR analyst, people analytics team, or business leadership monitors attrition and plans retention strategy.

## Objective

To turn raw HR records into four answers leadership actually needs:
1. How big is our attrition problem, and where is it concentrated?
2. Which departments and job roles need retention focus first?
3. Are overtime, low satisfaction, or poor work-life balance driving people out?
4. Which currently-employed people are at High risk of leaving next?

## Tools Used

- **Power BI Desktop** — data modeling, DAX, dashboard build
- **Power Query** — data cleaning and transformation
- **Microsoft Excel** — source dataset
- **DAX (Data Analysis Expressions)** — KPI and measure logic
- **GitHub** — version control and portfolio hosting

## Dataset Description

`HR_Attrition_Dataset.xlsx` contains 150 employee records with 22 columns:

| Column | Description |
|---|---|
| Employee ID | Unique employee identifier |
| Employee Name | Employee's full name |
| Age | Employee age |
| Gender | Male / Female |
| Department | Sales, Engineering, HR, Finance, Marketing, Operations, Customer Support |
| Job Role | Specific role within the department |
| Education Level | High School / Bachelor's / Master's / PhD |
| Marital Status | Single / Married / Divorced |
| Location | Employee's city |
| Joining Date | Date the employee joined |
| Years at Company | (Analysis Date − Joining Date) ÷ 365 |
| Monthly Income | Monthly salary |
| Performance Rating | 1 (lowest) to 5 (highest) |
| Training Hours | Training hours completed |
| Overtime Status | Yes / No |
| Work Mode | Office / Hybrid / Remote |
| Job Satisfaction Score | 1–10 |
| Work-Life Balance Score | 1–10 |
| Promotion Last 2 Years | Yes / No |
| Absenteeism Rate | % of working days absent |
| Attrition Status | Yes (has left) / No (still employed) |
| Attrition Risk Level | Low / Medium / High — rule-based score from satisfaction, work-life balance, overtime, and promotion history |

`Years at Company` and `Attrition Risk Level` are live Excel formulas, driven off an **Analysis Date** reference cell (`X2` on the `HR_Data` sheet, set to 2026-01-01). The risk formula is intentionally simple and transparent (no black-box model) — see `docs/DAX_MEASURES.md` for the exact logic and how to rebuild it as a DAX measure.

A second file, `Raw_Dataset_Before_Cleaning.xlsx`, is the same data before cleanup — it deliberately contains null values, inconsistent text casing, extra whitespace, and duplicate rows for the Power Query cleaning walkthrough.

## Power Query Steps

See [`docs/POWER_QUERY_STEPS.md`](docs/POWER_QUERY_STEPS.md) for the full click-by-click walkthrough. Summary: remove nulls, fix casing, trim whitespace, remove duplicates, correct data types, create Age Groups and Experience Bands, derive Month/Year from Joining Date.

## DAX Measures

See [`docs/DAX_MEASURES.md`](docs/DAX_MEASURES.md) for every measure with its formula and a plain-language explanation. Includes: Total Employees, Attrition Count, Attrition Rate %, Average Monthly Income, Average Job Satisfaction Score, Average Work-Life Balance Score, Department-wise Attrition, Job Role-wise Attrition, Overtime Employee Count, High Attrition Risk Employees Count, Average Tenure.

## Dashboard Features

- **KPI cards:** Total Employees, Attrition Count, Attrition Rate %, Average Satisfaction, Average Income
- **Bar chart:** Attrition by Department
- **Column chart:** Attrition by Job Role
- **Donut chart:** Attrition Status distribution
- **Line chart:** Attrition trend over time (by joining year/month)
- **Stacked bar chart:** Attrition by Work Mode / Overtime Status
- **Matrix table:** Department × Employees × Attrition Count × Attrition Rate
- **Slicers:** Department, Gender, Work Mode, Risk Level, Job Role
- **Corporate color theme:** blue for neutral metrics, green for retained/low risk, orange/red for attrition and high risk

## Key Insights

*(Fill in with your actual numbers once you build the dashboard — sample structure below)*

- Which department has the highest attrition rate, not just the highest attrition count
- Whether overtime employees churn at a meaningfully higher rate than non-overtime employees
- Whether low satisfaction or low work-life balance correlates more strongly with attrition in this data
- Which job roles carry the most "High" risk employees right now
- Whether promotion history (or lack of it) shows up as a retention factor

## Screenshots

Add dashboard screenshots here after building in Power BI Desktop:

```
screenshots/
  01-full-dashboard.png
  02-kpi-cards.png
  03-attrition-by-department.png
  04-attrition-trend.png
  05-risk-breakdown.png
```

`![Dashboard Overview](screenshots/01-full-dashboard.png)`

## Repository Structure

```
hr-workforce-attrition-dashboard/
├── README.md
├── HR_Attrition_Dataset.xlsx
├── Raw_Dataset_Before_Cleaning.xlsx
├── HR-Workforce-Attrition-Dashboard.pbix   (add after building in Power BI Desktop)
├── docs/
│   ├── POWER_QUERY_STEPS.md
│   ├── DAX_MEASURES.md
│   ├── PROJECT_OVERVIEW.md
│   ├── RESUME_DESCRIPTIONS.md
│   ├── LINKEDIN_CONTENT.md
│   └── PROJECT_CHECKLIST.md
└── screenshots/
    └── (dashboard images go here)
```

## Conclusion

This project demonstrates a full HR analytics workflow: messy raw data → cleaned and modeled data → DAX-driven attrition KPIs → a decision-ready dashboard. It reflects the kind of workforce monitoring tool used by HR analysts and people analytics teams to spot attrition risk early and target retention effort where it matters.
