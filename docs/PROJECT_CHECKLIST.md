# GitHub Setup and Final Checklist

## Repository name and description

**Repository name:** `hr-workforce-attrition-dashboard`

**One-line description:** Power BI dashboard tracking employee attrition and flagging at-risk employees across departments, roles, and work modes — built for HR analyst and people analytics-style workforce monitoring.

## GitHub upload steps (beginner-friendly)

1. Go to **github.com** and create a free account if you don't already have one (click **Sign up**, follow the prompts).
2. Once logged in, click the **+** icon in the top-right corner → **New repository**.
3. In **Repository name**, type `hr-workforce-attrition-dashboard`.
4. In **Description**, paste the one-line description above.
5. Select **Public** (not Private) — recruiters need to view it without logging in.
6. Leave "Add a README file" unchecked if you're uploading the one already prepared in this project (to avoid a conflict); check it only if you plan to write your own from scratch.
7. Click **Create repository**.
8. On the new repository's page, click **Add file → Upload files**.
9. Drag and drop (or click "choose your files" and select): `README.md`, `HR_Attrition_Dataset.xlsx`, `Raw_Dataset_Before_Cleaning.xlsx`, the entire `docs` folder, the `screenshots` folder (once you have images in it), and your `.pbix` file once it's built.
10. Scroll down, type a commit message such as "Initial commit: HR Workforce Attrition Dashboard".
11. Click **Commit changes**.

## Files to upload to GitHub

- [ ] `HR-Workforce-Attrition-Dashboard.pbix` (save this from Power BI Desktop after you finish building — File → Save As)
- [ ] `HR_Attrition_Dataset.xlsx` (clean dataset — already included in this zip)
- [ ] `Raw_Dataset_Before_Cleaning.xlsx` (optional, but shows you can clean real data — already included)
- [ ] `README.md` (already included)
- [ ] `docs/` folder — Power Query steps, DAX measures, report build guide, project overview, resume/LinkedIn content (already included)
- [ ] Dashboard screenshots (create a `screenshots/` folder and add PNGs after building)
- [ ] Optional: PDF export of the dashboard (**File → Export → Export to PDF** in Power BI Desktop)
- [ ] Optional: a one-page project summary for recruiters who won't open the full README

## Adding screenshots to the README

1. In Power BI Desktop, once your dashboard looks finished, go to **File → Export → Export to Image**, or use a screenshot tool (Snipping Tool on Windows, Cmd+Shift+4 on Mac) to capture the full report page.
2. Create a folder named `screenshots` inside your local project folder if it doesn't already exist (it's already included, empty, in this zip).
3. Save your images into it with clear names, e.g. `01-full-dashboard.png`, `02-kpi-cards.png`.
4. Upload that `screenshots` folder to GitHub the same way you uploaded everything else.
5. In `README.md`, reference an image using Markdown syntax:
   `![Dashboard Overview](screenshots/01-full-dashboard.png)`
6. This will render the actual image directly on your GitHub repo's front page.

## Final checklist before publishing

- [ ] Dataset loads cleanly into Power BI with no Power Query errors
- [ ] All DAX measures return correct, non-error values (spot-check a few against the `KPI_Summary` sheet in the Excel file)
- [ ] Every visual has a clear title and correctly formatted currency/percentage values
- [ ] All five slicers (Department, Gender, Work Mode, Risk Level, Job Role) are tested — filtering by each one updates every visual correctly
- [ ] Dashboard is visually consistent — one font, one color theme, aligned and evenly spaced visuals
- [ ] README.md is complete and every link to a file in `docs/` actually works
- [ ] Screenshots are uploaded and displaying correctly on the GitHub repo page
- [ ] Repository visibility is set to **Public**
- [ ] LinkedIn post drafted, with the GitHub link ready to paste into the first comment
