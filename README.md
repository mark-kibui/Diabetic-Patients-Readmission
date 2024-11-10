# Diabetes Readmission Prediction

## Project Overview
This project aims to predict the likelihood of a diabetes patient being readmitted to the hospital within 30 days, based on their medical history and hospital data.

## Table of Contents
1. [Introduction](#introduction)
2. [Data](#data)
3. [Data Preprocessing](#data-preprocessing)
4. [Exploratory Data Analysis](#exploratory-data-analysis)
5. [Feature Engineering](#feature-engineering)
6. [Modeling](#modeling)
7. [Evaluation](#evaluation)
8. [Conclusion](#conclusion)

## Introduction
The goal of this project is to develop a machine learning model that predicts patient readmission risk based on their medical and hospitalization records.

## Data
The dataset consists of various features related to diabetes patients, including:
- Encounter ID, Patient number, Race, Gender, Age
- Admission details: Type, Source, Time in hospital, Discharge disposition
- Medical history: Number of lab procedures, Diagnoses, Glucose test results, A1c test results
- Medication details: Diabetes medications, Changes in medications
- Readmission status: Readmitted (<30 days, >30 days, No readmission)

## Data Preprocessing
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