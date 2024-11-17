# Diabetes Readmission Prediction

## Project Overview
This project aims to predict the likelihood of a diabetes patient being readmitted to the hospital within 30 days, based on their medical history and hospital data.

## Table of Contents
1. [Introduction](#Introduction)
2. [Data](#Data)
3. [Data Understanding](#Data Understanding)
4. [Exploratory Data Analysis](#Exploratory-data-analysis)
5. [Feature Analysis and Engineering](#Feature Analysis and Engineering)
6. [Modeling and Evaluation](#Modeling and Evaluation)
7. [Conclusion and Recommendation](#Conclusion and Recommendation)

## Introduction
Hospital re-admission can indicate issues in patient care and may reveal areas where medical treatment could be improved. Predicting whether a patient will be readmitted allows healthcare providers to adapt treatments proactively, potentially reducing readmission rates and improving patients' outcome. This project focuses on identifying factors associated with readmissions in diabetic patients and aims to build a model to predict readmission risks.
### Problem Statement
In this dataset, I aim to predict one of three possible patient outcomes:

1. No Readmission: The patient was not readmitted after discharge.

2. Readmission in Less than 30 Days: Early readmission suggests potential issues with the initial treatment, which could be adjusted to reduce recurrence.

3. Readmission in More than 30 Days: While less severe than early readmission, this still suggests potential follow-up care adjustments based on the patient's condition.

The objective of the project is to develop models that predict these readmission categories, enabling more proactive and effective patient care strategies.

## Data

The dataset consists of various features related to diabetes patients, including:
- Encounter ID, Patient number, Race, Gender, Age
- Admission details: Type, Source, Time in hospital, Discharge disposition
- Medical history: Number of lab procedures, Diagnoses, Glucose test results, A1c test results
- Medication details: Diabetes medications, Changes in medications
- Readmission status: Readmitted (<30 days, >30 days, No readmission)
More about the data can be found here: https://onlinelibrary.wiley.com/doi/10.1155/2014/781670


| Feature                     | Type     | Description                                                                                                                                                                                                                                                                                                    |
|-----------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Encounter ID**            | Numeric  | Unique identifier of an encounter                                                                                                                                                                                                                                                                              |
| **Patient number**          | Numeric  | Unique identifier of a patient                                                                                                                                                                                                                                                                                 |
| **Race**                    | Nominal  | Values: Caucasian, Asian, African American, Hispanic, and other                                                                                                                                                                                                                                               |
| **Gender**                  | Nominal  | Values: male, female, and unknown/invalid                                                                                                                                                                                                                                                                      |
| **Age**                     | Nominal  | Grouped in 10-year intervals: [0, 10), [10, 20), …, [90, 100)                                                                                                                                                                                                                                                 |
| **Weight**                  | Numeric  | Weight in pounds.                                                                                                                                                                                                                                                                                             |
| **Admission type**          | Nominal  | Integer identifier corresponding to 9 distinct values, e.g., emergency, urgent, elective, newborn, and not available                                                                                                                                                                                          |
| **Discharge disposition**    | Nominal  | Integer identifier corresponding to 29 distinct values, e.g., discharged to home, expired, and not available                                                                                                                                                                                                   |
| **Admission source**         | Nominal  | Integer identifier corresponding to 21 distinct values, e.g., physician referral, emergency room, and transfer from a hospital                                                                                                                                                                                |
| **Time in hospital**        | Numeric  | Integer number of days between admission and discharge                                                                                                                                                                                                                                                        |
| **Payer code**              | Nominal  | Integer identifier corresponding to 23 distinct values, e.g., Blue Cross/Blue Shield, Medicare, and self-pay                                                                                                                                                                                                  |
| **Medical specialty**       | Nominal  | Integer identifier of the admitting physician's specialty, corresponding to 84 distinct values, e.g., cardiology, internal medicine, family/general practice, and surgeon                                                                                                                                       |
| **Number of lab procedures**| Numeric  | Number of lab tests performed during the encounter                                                                                                                                                                                                                                                             |
| **Number of procedures**    | Numeric  | Number of procedures (other than lab tests) performed during the encounter                                                                                                                                                                                                                                     |
| **Number of medications**   | Numeric  | Number of distinct generic names administered during the encounter                                                                                                                                                                                                                                            |
| **Number of outpatient visits** | Numeric  | Number of outpatient visits of the patient in the year preceding the encounter                                                                                                                                                                                                                              |
| **Number of emergency visits** | Numeric | Number of emergency visits of the patient in the year preceding the encounter                                                                                                                                                                                                                                |
| **Number of inpatient visits**  | Numeric | Number of inpatient visits of the patient in the year preceding the encounter                                                                                                                                                                                                                                |
| **Diagnosis 1**             | Nominal  | The primary diagnosis (coded as the first three digits of ICD9); 848 distinct values                                                                                                                                                                                                                          |
| **Diagnosis 2**             | Nominal  | Secondary diagnosis (coded as the first three digits of ICD9); 923 distinct values                                                                                                                                                                                                                            |
| **Diagnosis 3**             | Nominal  | Additional secondary diagnosis (coded as the first three digits of ICD9); 954 distinct values                                                                                                                                                                                                                 |
| **Number of diagnoses**     | Numeric  | Number of diagnoses entered into the system                                                                                                                                                                                                                                                                    |
| **Glucose serum test result** | Nominal | Indicates the range of the result or if the test was not taken. Values: “>200,” “>300,” “normal,” and “none” if not measured                                                                                                                                                                                  |
| **A1c test result**         | Nominal  | Indicates the range of the result or if the test was not taken. Values: “>8” if the result was greater than 8%, “>7” if the result was between 7% and 8%, “normal” if less than 7%, and “none” if not measured.                                                                                                |
| **Change of medications**   | Nominal  | Indicates if there was a change in diabetic medications (either dosage or generic name). Values: “change” and “no change”                                                                                                                                                                                     |
| **Diabetes medications**    | Nominal  | Indicates if any diabetic medication was prescribed. Values: “yes” and “no”                                                                                                                                                                                                                                  |
| **24 features for medications** | Nominal | For 24 generic names (e.g., metformin, insulin, glyburide-metformin), indicates whether the drug was prescribed or if there was a change in dosage. Values: “up” if dosage increased, “down” if decreased, “steady” if unchanged, and “no” if not prescribed |
| **Readmitted**              | Nominal  | Days to inpatient readmission. Values: “<30” if readmitted within 30 days, “>30” if readmitted after 30 days, and “No” if not readmitted                                                                                                                                |

## Data Understanding
- Handling missing values
- Encoding categorical variables
- Scaling numeric features
- Splitting data into training and test sets

## Exploratory Data Analysis
- Distribution of readmission status
- Correlation between features
- Visualizations for patient demographics (e.g., Race, Gender, Age)
- Medical history insights (e.g., Glucose serum test, A1c test)

## Feature Engineering
- Creating new features based on the existing data (e.g., calculating age from age ranges)
- One-hot encoding for categorical features like Race, Gender, and Diagnosis codes

## Modeling
- Model selection: Logistic Regression, Decision Trees, Random Forest, XGBoost
- Hyperparameter tuning for optimal performance
- Model training on the prepared dataset

## Evaluation
- Metrics: Accuracy, Precision, Recall, F1-score, AUC-ROC
- Cross-validation to assess model robustness
- Evaluation on the test set

## Conclusion
The project successfully builds a predictive model to estimate diabetes patient readmission risk. Further improvements could include refining feature engineering and exploring additional models or ensemble methods for better accuracy.