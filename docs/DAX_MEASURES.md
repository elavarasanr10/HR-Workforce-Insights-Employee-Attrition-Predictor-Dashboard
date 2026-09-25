# DAX Measures

Create each of these under **Home → New Measure** (with the `HR_Data` table selected in the Fields pane), or right-click the table name → **New Measure**. Put them all into a dedicated `_Measures` table for a clean model: **Modeling → New Table**, type just `_Measures = {}`, then for each measure below use its properties pane (or drag it in the Fields list) to move it into `_Measures`.

## Core workforce measures

**Total Employees**
```
Total Employees = DISTINCTCOUNT('HR_Data'[Employee ID])
```
Counts unique employees, not rows — protects the number if a record is ever duplicated.

**Attrition Count**
```
Attrition Count = CALCULATE([Total Employees], 'HR_Data'[Attrition Status] = "Yes")
```
How many employees in the current filter context have left the company.

**Attrition Rate %**
```
Attrition Rate % = DIVIDE([Attrition Count], [Total Employees], 0)
```
Attrition Count as a share of Total Employees. `DIVIDE` returns 0 instead of an error if a filtered slice has zero employees.

**Average Monthly Income**
```
Average Monthly Income = AVERAGE('HR_Data'[Monthly Income])
```

**Average Job Satisfaction Score**
```
Average Job Satisfaction Score = AVERAGE('HR_Data'[Job Satisfaction Score])
```

**Average Work-Life Balance Score**
```
Average Work-Life Balance Score = AVERAGE('HR_Data'[Work-Life Balance Score])
```

## Breakdown measures

**Department-wise Attrition**
```
Department-wise Attrition = CALCULATE([Attrition Count], ALLEXCEPT('HR_Data', 'HR_Data'[Department]))
```
Forces the attrition count to always break down by Department regardless of what other slicers are active — this is what powers the "Attrition by Department" bar chart and the "department with highest attrition" insight.

**Job Role-wise Attrition**
```
Job Role-wise Attrition = CALCULATE([Attrition Count], ALLEXCEPT('HR_Data', 'HR_Data'[Job Role]))
```
Same pattern, applied to Job Role instead of Department.

**Overtime Employee Count**
```
Overtime Employee Count = CALCULATE([Total Employees], 'HR_Data'[Overtime Status] = "Yes")
```
How many currently-tracked employees work overtime — compare this against the Attrition Rate % for overtime vs. non-overtime employees to test whether overtime is actually linked to attrition in this data.

**High Attrition Risk Employees Count**
```
High Attrition Risk Employees Count = CALCULATE([Total Employees], 'HR_Data'[Attrition Risk Level] = "High")
```
Counts employees currently flagged "High" risk — since Attrition Risk Level is a rule-based score built from satisfaction, work-life balance, overtime, and promotion history (see the README), this measure surfaces who to focus retention effort on right now.

**Average Tenure**
```
Average Tenure = AVERAGE('HR_Data'[Years at Company])
```
Average years at the company across the current filter context — useful for comparing tenure between departments, or between employees who left vs. stayed.

## Helper measures for KPI cards and insights

**Department with Highest Attrition**
```
Department with Highest Attrition =
VAR RankedDepartments =
    TOPN(1, VALUES('HR_Data'[Department]), CALCULATE([Attrition Rate %]), DESC)
RETURN
    CONCATENATEX(RankedDepartments, 'HR_Data'[Department])
```
Returns the single department with the highest attrition *rate* (not just count) — important because a big department can have a high attrition count while actually having a low rate.

**Role with Highest Attrition**
```
Role with Highest Attrition =
VAR RankedRoles =
    TOPN(1, VALUES('HR_Data'[Job Role]), CALCULATE([Attrition Rate %]), DESC)
RETURN
    CONCATENATEX(RankedRoles, 'HR_Data'[Job Role])
```
Same logic, applied to Job Role.

**Attrition Rate % — Overtime vs. No Overtime** (two separate measures, useful side by side on a chart)
```
Attrition Rate % (Overtime) =
CALCULATE([Attrition Rate %], 'HR_Data'[Overtime Status] = "Yes")

Attrition Rate % (No Overtime) =
CALCULATE([Attrition Rate %], 'HR_Data'[Overtime Status] = "No")
```
Put both on the same visual to directly test whether overtime employees leave at a higher rate.
