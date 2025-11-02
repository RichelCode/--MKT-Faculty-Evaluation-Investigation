# Effects of Professor Performance and Student Behavior on Teaching Evaluations (Miami University MKT)

This repository contains the analysis for the study **"Effects of Professor Performance and Student Behavior on Overall Teaching Evaluation in Marketing Courses at Miami University"**. The goal of the project is to understand which instructor-level and student-level factors most strongly predict students’ **overall instructor rating (iRating)** in Marketing (MKT) courses.

## Project Summary

Student Evaluations of Teaching (SETs) are widely used for promotion, annual reviews, and course improvement. Yet it is not always clear whether students are responding more to **what the professor does** (clarity, preparedness, enthusiasm) or to **how students behave/engage in the course** (attendance, participation, effort). This project builds a set of nested mixed-effects models to separate and compare these effects. 

We specifically examined:

1. **Professor performance measures** (15 items prefixed with `i...`)
2. **Student behavior measures** (6 items prefixed with `s...`)
3. **Course type** as a moderator (core vs elective) 

## Research Questions

1. **Do professor performance measures significantly predict the overall instructor rating (iRating)?**
2. **Do student behavior/engagement measures add extra explanatory power once professor measures are in the model?**
3. **Do these relationships change by course type (core vs elective)?**
---

## Data

- **Source**: Student evaluation data from *all* Marketing (MKT) course sections at **Miami University**.
- **Years covered**: **Fall 2013 to Spring 2017**.
- **Unit of analysis**: Aggregated by **course section**, with instructor IDs anonymized.
- **Variables:**
  - **Dependent variable**: `iRating` (Overall instructor rating), 0–4 scale  
    - 0 = Unsatisfactory  
    - 1 = Poor  
    - 2 = Average  
    - 3 = Good  
    - 4 = Excellent :contentReference[oaicite:8]{index=8}
  - **Professor performance** (about 14–15 items), e.g.:
    - `iPrepared` (was the instructor well prepared?)
    - `iChallenged` (did the instructor challenge students to think?)
    - `iWelQues` (was the instructor welcoming to questions?)
    - `iEnthusiasm`  
    These were collected on a 0–4 agreement scale. :contentReference[oaicite:9]{index=9}
  - **Student behavior** (6 items, prefixed with `s`), e.g. `sEngaged_Z`, `sPositive_Z`. These capture how students behaved/engaged in the course.
  - **Moderator**: `CourseType` (core vs elective).

> **Important**: The original data cannot be shared publicly because it contains internal course evaluation records. In this repo, please share only de-identified or simulated data, or the R Markdown workflow.

---

## Methods

The analysis was done in **R** using an **R Markdown** workflow (`.Rmd` → `.html`). The core approach was to estimate **nested linear mixed-effects models** and compare them with **Likelihood Ratio Tests (LRT)** to see whether adding a block of variables significantly improves model fit. 
**Model progression:**

1. **Model 1**: Random intercept model with professor performance measures.  
   - Answered: Do instructor actions matter?
2. **Model 2**: Model 1 + student behavior measures.  
   - Result: Adding student behavior **significantly improved** model fit (p = 0.0092). This means that even after accounting for how good the professor was, engaged/positive students still give higher overall ratings. 
3. **Model 3**: Model 2 + course type.  
   - Result: Course type **by itself** did not significantly improve model fit (p = 1). 
4. **Model 4**: Model 3 + interactions between course type and all predictors.  
   - Result: This **did** significantly improve fit (p = 0.0054), so the size of the effect of professor performance and student behavior depends on course type. 

This stepwise setup shows **where** the variance in student ratings is coming from rather than trying to build a single “best” predictive model.

---

## Key Findings

- Professor performance variables such as **instructor quality, challenge, preparation, and ability to handle questions** were strongly and positively associated with higher overall ratings. 
- Student behavior variables **still mattered** after that, which suggests that SET scores are a mixture of teacher behavior and student engagement. 
- Course type alone did not explain much, but allowing the model to vary by course type showed that **the effects are not identical in core vs elective courses.** 
- Descriptive plots in the report showed that instructor items had relatively high means, but the overall rating was lower and more variable, which supports the need for modeling. 

---

## Repository Structure

```text
.
├── README.md                  # You are here
├── MKT_Rongrong_RICHEL_final_report.Rmd   # Source analysis file (R Markdown)
├── MKT_Rongrong_RICHEL_final_report.html  # Rendered report
├── data/
│   ├── raw/                   # (Not committed) Original SET data, restricted
│   └── processed/             # (Optional) Cleaned or simulated data
├── R/
│   ├── 01_load_libraries.R
│   ├── 02_load_and_clean_data.R
│   ├── 03_descriptives.R
│   ├── 04_mixed_models.R
│   └── 05_plots.R
└── output/
    ├── figures/
    └── tables/
