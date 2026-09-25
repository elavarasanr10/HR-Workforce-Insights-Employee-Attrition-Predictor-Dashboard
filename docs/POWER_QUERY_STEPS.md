# Power Query Steps (Beginner-Friendly, Click-by-Click)

This walkthrough assumes you have never opened Power Query before. Follow every step in order — don't skip ahead.

## Step 1 — Open Power BI Desktop and load the file

1. Open **Power BI Desktop**.
2. On the Home ribbon, click **Get Data**.
3. In the dropdown, click **Excel workbook**.
4. Browse to and select `Raw_Dataset_Before_Cleaning.xlsx` (use this file so you get real cleaning practice — if you'd rather skip straight to a clean model, use `HR_Attrition_Dataset.xlsx` instead and jump to Step 9).
5. Click **Open**.
6. In the Navigator window that pops up, tick the checkbox next to **Raw_Data**.
7. Click **Transform Data** (not "Load" — this opens the Power Query Editor where all the cleaning happens).

## Step 2 — Remove null values

The raw file has a few blank cells in **Department** and **Training Hours**.

1. In the Power Query Editor, click the column header for **Department**.
2. Right-click the header → click **Remove Empty**. This deletes any row where Department is blank, since a missing department breaks every department-based visual.
3. Click the column header for **Training Hours**.
4. Right-click the header → click **Replace Values**.
5. In the "Value To Find" box, leave it blank (this targets null). In "Replace With," type `0`.
6. Click **OK**. This keeps the employee's row (their other data is still valid) but treats a missing training hours figure as zero instead of leaving a gap.

## Step 3 — Fix inconsistent text casing

Some **Department** values came in as lowercase (e.g. `engineering` instead of `Engineering`).

1. Click the column header for **Department**.
2. On the ribbon, go to **Transform → Format → Capitalize Each Word**.
3. Every value in that column now starts with a capital letter consistently.

## Step 4 — Trim extra whitespace

Some **Location** values have extra spaces, like `"  Pune "` instead of `"Pune"`. These invisible spaces make Power BI treat them as different categories.

1. Click the column header for **Location**.
2. Go to **Transform → Format → Trim**.
3. This removes leading and trailing spaces from every value in the column.

## Step 5 — Remove duplicate rows

1. Click the top-left corner cell (or press **Ctrl+A** while your cursor is in a column header area) to select all columns.
2. Go to **Home → Remove Rows → Remove Duplicates**.
3. Power Query keeps only the first occurrence of any row where every column matches exactly — this removes the accidental duplicate records in the raw file.

## Step 6 — Fix data types

Power Query sometimes guesses a column's type wrong. Check each one and correct it:

1. Look at the small icon on the left side of each column header (ABC = text, 123 = number, calendar = date).
2. Click that icon to change the type if it's wrong. Set these specifically:
   - **Joining Date** → Date
   - **Age, Performance Rating, Training Hours** → Whole Number
   - **Monthly Income, Absenteeism Rate** → Decimal Number
   - **Everything else** (Employee ID, Employee Name, Gender, Department, Job Role, Education Level, Marital Status, Location, Overtime Status, Work Mode, Job Satisfaction Score, Work-Life Balance Score, Promotion Last 2 Years, Attrition Status) → Text or Whole Number as appropriate (satisfaction/work-life balance scores should be Whole Number since they're 1–10 ratings)
3. If Power BI shows a warning about "changed type," click **Replace Current** when prompted.

## Step 7 — Create Age Groups

This turns a raw number (Age) into a readable bucket for slicers and visuals.

1. Go to **Add Column → Custom Column**.
2. Name the new column `Age Group`.
3. Enter this formula:
   ```
   if [Age] < 25 then "Under 25"
   else if [Age] < 35 then "25-34"
   else if [Age] < 45 then "35-44"
   else if [Age] < 55 then "45-54"
   else "55+"
   ```
4. Click **OK**.

## Step 8 — Create Experience Bands

Similarly, turn tenure into readable bands. If you're working from the raw file (no `Years at Company` column yet), first add a column for it:

1. Go to **Add Column → Custom Column**, name it `Years at Company`, formula:
   ```
   Number.Round(Duration.Days(DateTime.LocalNow() - [Joining Date]) / 365, 1)
   ```
   (In the finished `HR_Attrition_Dataset.xlsx`, this is already calculated in Excel using a fixed Analysis Date — see the README — so you can skip straight to the band step below if you loaded that file.)
2. Go to **Add Column → Custom Column** again, name it `Experience Band`, formula:
   ```
   if [Years at Company] < 2 then "0-2 Years"
   else if [Years at Company] < 5 then "2-5 Years"
   else if [Years at Company] < 10 then "5-10 Years"
   else "10+ Years"
   ```
3. Click **OK**.

## Step 9 — Format the Joining Date field

1. Confirm **Joining Date** is set to type **Date** (done in Step 6).
2. Any display formatting (e.g. `dd-mmm-yyyy`) is applied later in Report view, not in Power Query — Power Query only needs the correct underlying type.

## Step 10 — Create Month and Year columns from Joining Date

These power the "Attrition trend over time" line chart.

1. Click the **Joining Date** column header to select it.
2. Go to **Add Column → Date → Month → Name of Month**. This adds a `Month` column.
3. Click **Joining Date** again.
4. Go to **Add Column → Date → Year → Year**. This adds a `Year` column.

## Step 11 — Confirm calculated columns

`Years at Company` and `Attrition Risk Level` are already present as formula-driven columns in `HR_Attrition_Dataset.xlsx` (see the README for the exact logic and the Analysis Date reference cell). If you built these yourself in Power Query in Steps 7–8, you're covered. If you want `Attrition Risk Level` reproduced in Power Query rather than relying on the Excel formula, add one more custom column:

```
let
    riskScore = (10 - [Job Satisfaction Score]) + (10 - [Work-Life Balance Score])
        + (if [Overtime Status] = "Yes" then 3 else 0)
        + (if [Promotion Last 2 Years] = "No" then 2 else 0)
in
    if riskScore >= 14 then "High"
    else if riskScore >= 8 then "Medium"
    else "Low"
```

## Step 12 — Close & Apply

1. Go to **Home → Close & Apply**.
2. Power BI loads the cleaned table into the data model. You're ready to move on to `DAX_MEASURES.md`.
