# CareLoop Clinics — No-Show Guard

**Project Repository:** https://github.com/sairevanth1/careloop-no-show-guard

## Project Overview

CareLoop Clinics — No-Show Guard is an end-to-end data analytics and machine learning project designed to understand and predict missed medical appointments across eight outpatient clinics.

The project uses Python, SQL, Machine Learning and Generative AI to clean appointment records, identify patterns in missed appointments, predict high-risk bookings and analyse patient follow-up notes.

## Key Findings

- **Part 1 — Data Cleaning:** Processed 1,020 raw appointment records and produced 990 cleaned records after removing duplicates and handling missing and invalid values.
- **Part 2 — SQL Analysis:** Appointments booked 31 or more days in advance had a 60.5% no-show rate, compared with 16.2% for appointments booked 1–7 days in advance.
- **Part 3 — Machine Learning:** Logistic Regression achieved a test ROC-AUC of 0.7889. At a threshold of 0.35, it achieved 57.1% recall and flagged 49 of 198 test appointments.
- **Part 4 — Generative AI:** Gemini successfully analysed nine non-blank follow-up notes. Both notes classified as forgotten or missing reminders belonged to appointments with no recorded reminder.

## Model Selection

Three machine learning approaches were evaluated: Logistic Regression, Decision Tree and Random Forest.

Logistic Regression was selected based on its cross-validated ROC-AUC of approximately 0.77, the highest among the evaluated models.

A threshold of 0.35 was selected using out-of-fold training predictions because it provided a better balance between precision and recall than the default 0.50 threshold.

Final test-set performance:

- Accuracy: 78.79%
- Precision: 57.14%
- Recall: 57.14%
- F1-score: 57.14%
- ROC-AUC: 0.7889

The test set was reserved for final evaluation and was not used to select the model or threshold.

## Business Recommendation

CareLoop should prioritise appointments with higher predicted no-show risk for proactive follow-up calls on the evening before the appointment. The selected Logistic Regression model achieved a ROC-AUC of 0.7889 and recall of 57.1% at the 0.35 threshold, flagging 49 out of 198 test appointments. SQL analysis identified a 60.5% no-show rate for bookings made 31 or more days in advance, making long booking lead times an important risk indicator. The follow-up note analysis found that both patients classified as having forgotten or not received a reminder had no reminder recorded, while five of the ten analysed appointments had no reminder recorded. CareLoop should therefore prioritise high-risk calls, review reminder delivery and contact details, and investigate long-lead-time bookings. Future analysis should use a larger follow-up note sample to better understand the reasons behind missed appointments.

## Limitations

1. **Small follow-up sample:** Only ten follow-up notes were analysed. These notes are illustrative and cannot establish the actual reasons for no-shows across all clinics.
2. **Cleaning before splitting:** Medians, quartiles and outlier fences were calculated using all 990 records before the train/test split, creating a small indirect influence from test data.
3. **Random train/test split:** The same patient may appear in both training and test sets. The random split also does not represent a real-world past-to-future prediction scenario.

## Project Files

- 01_ingest_clean+03_model+04_genai.ipynb — Combined Python, machine learning and GenAI implementation.
- `02_queries.sql` — SQL queries and analysis.
- `load_data.sql` — SQL database loading statements.
- `appointments_clean.csv` — Cleaned appointment records.
- `clinics_enriched.csv` — Clinic data enriched with weather information.
- `rejected_rows.json` — Records rejected during initial validation.
- `test_risk_scores.csv` — Final machine learning risk predictions.
- `notes_analysed.csv` — Structured GenAI analysis of patient follow-up notes.
- `data/` — Original appointment, clinic and follow-up note datasets.

## Technologies Used

Python, Pandas, NumPy, Scikit-learn, SQL, MySQL, Google Gemini API, Pydantic and Google Colab.
