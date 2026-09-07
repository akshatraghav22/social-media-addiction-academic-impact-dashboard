# 📱 Students Social Media Addiction & Academic Impact — Power BI Analytics

`Visualization` **Power BI Desktop** | `Analytics` **Power Query · DAX** | `Domain` **Education & Behavioral Psychology** | `License` **MIT**

An end-to-end interactive Power BI business intelligence dashboard analyzing the empirical relationships between daily social media usage, academic performance, sleep patterns, mental health scores, and relationship conflict intensity across global student demographics.

---

## 📋 Business Problem & Objective

Academic administrators, educators, and student wellness counselors need empirical visibility into how digital media consumption affects student well-being. This project builds an interactive analytics platform to quantify:

- The prevalence and severity of social media addiction across academic levels (High School, Undergraduate, Graduate).
- The share of students experiencing negative academic performance consequences.
- The behavioral trade-offs between daily usage, sleep duration, and mental wellness indicators.
- Platform preference distributions across demographics and their link to relationship conflict.

---

## 📊 Dataset & Model Architecture

- **Source:** Comprehensive Student Social Media Addiction Survey (`Students Social Media Addiction.xlsx`)
- **Scope:** 705 student records across 110 countries, ages 18–24
- **Relational schema:** Two tables joined on `Student_ID`:

| Table | Fields |
|---|---|
| **Student Details** | `Student_ID`, `Age`, `Gender`, `Academic_Level`, `Country`, `Sleep_Hours_Per_Night`, `Mental_Health_Score`, `Relationship_Status`, `Conflicts_Over_Social_Media`, `Addicted_Score` |
| **Platform Details** | `Student_ID`, `Avg_Daily_Usage_Hours`, `Most_Used_Platform`, `Affects_Academic_Performance` |

---

## 📈 Dashboard Highlights

### 1. Executive Overview & Mental Health

| Executive Overview | Mental Health & Lifestyle |
|---|---|
| ![Executive Overview](dashboard_overview.png) | ![Mental Health & Lifestyle](Mental%20Health%20%26%20Lifestyle.png) |
| KPI cards (705 students, 64.3% academically affected, 4.92h avg usage, 6.87h avg sleep, 199 high-risk), Addiction Score by Academic Level, Avg Usage Hours by Age, and Gender split. | Addicted Score vs. Mental Health Score scatter, Country × Mental Health Band matrix, and Avg Sleep Hours by Age (18–24). |

### 2. Academic Impact & Relationship Dynamics

| Academic Impact | Relationships & Conflicts |
|---|---|
| ![Academic Impact](Academic_Impact.png) | ![Relationships and Conflicts](Relationships%20and%20Conflicts.png) |
| Avg Daily Usage by Academic Level (High School: 5.5h, Undergrad: 5.0h, Grad: 4.8h) and Academic Performance Impact by Platform (Affected vs. Not Affected). | Student-wise addiction score table, Conflict Level by Relationship Status, and Relationship Status distribution (54.5% Single, 41.0% In Relationship, 4.5% Complicated). |

### 3. Interactive Story View & Drill-Through Profiles

| Interactive Story View | Drill-Through Student Profile |
|---|---|
| ![Interactive Story View](Interactive%20Story%20View.png) | ![Drill Through Student Profile](Drill%20Through%20Student%20Profile.png) |
| Toggle-driven demographic perspectives: Avg Daily Usage Hours by Gender and Most Used Platform breakdown by gender. | Granular student profile card matrix: Age, Gender, Country, Academic Level, Avg Daily Usage, Most Used Platform, Addicted Score, Sleep Hours, Mental Health Score, Conflicts, Relationship Status, and Conflict Level. |

---

## 🔬 Methodology & DAX Engineering

1. **Data Modeling:** Cleaned and normalized survey responses into a two-table model (`Student Details`, `Platform Details`) with an active one-to-one relationship on `Student_ID`. Handled missing values, removed duplicates, and validated data types/ranges in Power Query.

2. **Key DAX Measures & Formulations:**

   **% Academically Impacted:**
   ```dax
   % Affected Academically =
   DIVIDE(
       CALCULATE(COUNTROWS('Platform Details'), 'Platform Details'[Affects_Academic_Performance] = "Yes"),
       COUNTROWS('Platform Details')
   )
   ```

   **High-Risk Addiction Cohort** (`Addicted_Score > 7`):
   ```dax
   High Addiction =
   CALCULATE(
       COUNTROWS('Student Details'),
       'Student Details'[Addicted_Score] > 7
   )
   ```

   **Average Daily Usage & Sleep Metrics:**
   ```dax
   Avg Daily Usage = AVERAGE('Platform Details'[Avg_Daily_Usage_Hours])
   Avg Sleep Hours = AVERAGE('Student Details'[Sleep_Hours_Per_Night])
   ```

   **Mental Health Band** (calculated column, Poor ≤3, Average 4–6, Good ≥7):
   ```dax
   Health Band =
   SWITCH(
       TRUE(),
       'Student Details'[Mental_Health_Score] <= 3, "Poor",
       'Student Details'[Mental_Health_Score] <= 6, "Average",
       "Good"
   )
   ```

   **Conflict Level** (calculated column, Low 0–1, Medium 2–3, High ≥4):
   ```dax
   Conflict Level =
   SWITCH(
       TRUE(),
       'Student Details'[Conflicts_Over_Social_Media] <= 1, "Low",
       'Student Details'[Conflicts_Over_Social_Media] <= 3, "Medium",
       "High"
   )
   ```

3. **Interactive Slicers & Navigation:**
   - Universal slicers for Gender, Country, Academic Level, and Age Range (18–24 slider).
   - Toggle-driven Interactive Story View (Gender View vs. Academic Level View).
   - Drill-through page for granular individual student auditing.

---

## 🔍 Key Insights & Findings

- **Academic Hierarchy Risk:** High School students carry the highest average addiction score (**8.04 / 10**) and longest daily usage (**5.5 hrs**), compared to Undergraduates (**6.49 / 5.0 hrs**) and Graduates (**6.24 / 4.8 hrs**).
- **Widespread Academic Impact:** **64.3%** of surveyed students report negative effects on academic performance directly attributed to social media habits.
- **Platform Concentration:** Instagram (**35.3%**) and TikTok (**21.8%**) dominate total usage, together accounting for over **57%** of preferred platforms and driving the largest share of academic disruption (172 and 144 "Affected" respondents respectively).
- **Critical Risk Segment:** **199 of 705 students (28.2%)** fall into the high-risk addiction band (`Addicted_Score > 7`), correlating with lower mental health scores.
- **Relationship Conflict:** Students "In Relationship" report a higher share of Medium/High conflict levels tied to social media use compared to Single students, despite Single students being the largest group (54.5%).
- **Sleep Recovery Pattern:** Average sleep hours rise from 5.6h at age 18 to a peak of 7.13h at age 22, before tapering slightly — inversely tracking the dip in average usage hours over the same age range.

---

## 🛠️ Tools & Technologies

Excel · Power BI Desktop · Power Query · DAX

---

## 📁 Repo

[github.com/akshatraghav22/social-media-addiction-academic-impact-dashboard](https://github.com/akshatraghav22/social-media-addiction-academic-impact-dashboard)
