# Report Building & Dashboard Design — Beginner Walkthrough

This picks up after `DAX_MEASURES.md` — you should already have your cleaned table loaded and your measures created in a `_Measures` table before starting here.

## Step 1 — Set up the canvas

1. Switch to the **Report** view (the middle icon on the left sidebar in Power BI Desktop).
2. Click the blank canvas → go to the **Format** pane (paint roller icon) on the right → under **Canvas settings**, set page size to **16:9** (this is the default and matches the layout described below).
3. Go to **View → Themes** and pick a base theme close to corporate blue, or use **Format → Customize current theme** to manually set your color palette (see Step 6 below for the exact colors).

## Step 2 — Add the KPI cards (top section)

1. From the Fields pane, drag **Total Employees** onto the canvas. Power BI adds it as a table by default — click the **Card** visual icon in the Visualizations pane to convert it.
2. Resize it to a small rectangle and place it at the top-left of the canvas.
3. Repeat for **Attrition Count**, **Attrition Rate %**, **Average Job Satisfaction Score**, and **Average Monthly Income** — five cards total, placed in a single row across the top.
4. Select all five cards (click one, then Shift+click the rest) → use **Format → Align → Align Top** and **Distribute Horizontally** so they're evenly spaced.
5. Give each card a title matching its measure name via **Format pane → General → Title**.

## Step 3 — Add the middle-section charts

1. **Bar chart — Attrition by Department:** click the **Clustered Bar Chart** icon → drag **Department** to the Y-axis and **Attrition Count** (or **Department-wise Attrition**) to the X-axis (values).
2. **Column chart — Attrition by Job Role:** click **Clustered Column Chart** → drag **Job Role** to the X-axis and **Job Role-wise Attrition** to the Y-axis (values).
3. **Donut chart — Attrition Status distribution:** click **Donut Chart** → drag **Attrition Status** to Legend and **Total Employees** to Values.
4. **Line chart — Attrition trend over time:** click **Line Chart** → drag **Year** (and optionally **Month**) to the X-axis and **Attrition Count** to the Y-axis (values).
5. **Stacked bar chart — Attrition by Work Mode / Overtime Status:** click **Stacked Bar Chart** → drag **Work Mode** (or **Overtime Status**) to the Y-axis, **Attrition Status** to Legend, and **Total Employees** to Values.
6. Place these five visuals in the middle two-thirds of the canvas: bar and column charts side by side in one row, the line chart full-width in the next row, and the donut and stacked bar charts side by side in the row after that.

## Step 4 — Add the bottom section

1. Click the **Table** or **Matrix** visual icon.
2. Drag **Department** to Rows, and **Total Employees**, **Attrition Count**, and **Attrition Rate %** to Values.
3. Place this matrix at the bottom-left of the canvas.
4. Next to it, add a **Text Box** (Insert → Text Box) and type 3–4 plain-language insight bullets once you've reviewed the actual numbers (see the "Key Insights" section of the README for the categories to cover).

## Step 5 — Add slicers and filters (side panel)

1. Click the **Slicer** visual icon.
2. Drag **Department** into it. Repeat this for **Gender**, **Work Mode**, **Attrition Risk Level**, and **Job Role** — five separate slicer visuals.
3. Stack all five slicers vertically along the left or right edge of the canvas.
4. Optionally add a **Date Slicer** on **Joining Date** if you want to filter the whole report by joining period, placed above or below the other slicers.
5. Select all slicer visuals → **Format → Align → Align Left** (or Right) and **Distribute Vertically** so they line up cleanly.

## Step 6 — Apply the color theme

- **Corporate blue** (e.g. `#1F4E78`) for card backgrounds, chart axis lines, and neutral structural elements.
- **Green** (e.g. `#2E8B57`) for positive/retained indicators — low risk, low attrition.
- **Orange/Red** (e.g. `#E67E22` / `#C0392B`) for attrition counts, high-risk flags, and negative indicators.
- Apply this by selecting each visual → **Format pane → Colors**, and manually setting the data colors to match. For consistency, set Attrition Status = "Yes" segments to red/orange and "No" segments to green everywhere it appears (donut chart, stacked bar chart).

## Step 7 — Polish for a premium, recruiter-friendly look

1. **Font:** pick one font family (Segoe UI is the Power BI default and reads as clean/corporate) and apply it consistently via **Format → Text** on every visual — don't mix fonts.
2. **Alignment and spacing:** use **Format → Align** and **Distribute** (accessible after multi-selecting visuals) rather than eyeballing positions — this is what makes a dashboard look "designed" instead of "assembled."
3. **Chart sizing:** keep chart heights consistent within each row (e.g. the bar and column charts in Step 3 should be the same height).
4. **Icons:** if you want icons on KPI cards (e.g. a small headcount icon next to Total Employees), use Power BI's built-in icon sets under **Insert → Icons**, or add simple PNG icons matching your color theme — keep them small and consistent in style.
5. **Background:** a very light gray or white background reads as cleaner and more corporate than a heavily colored one — save the color for data, not decoration.
6. **Title:** add a report-level title text box at the very top (e.g. "HR Workforce Insights & Employee Attrition Dashboard") above the KPI card row.

## Step 8 — Test before exporting

1. Click through each slicer (try filtering by one Department, then by one Risk Level) and confirm every visual updates correctly.
2. Check that KPI cards show sensible numbers with no filters applied (should match the `KPI_Summary` sheet in the Excel file).
3. Fix any visual that doesn't respond to slicers — this is almost always a relationship issue in the data model (check **Model view** to confirm your Date table, if you added one, is properly related to `HR_Data` on the Joining Date column).
