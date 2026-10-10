Heart Disease Classification

A machine learning project that predicts whether a patient has heart disease from clinical measurements, using the Cleveland subset of the UCI Heart Disease dataset. Includes EDA, three classification models, model comparison, feature importance and a Power BI dashboard.

Disclaimer: This is an educational project. It is not a medical diagnostic system.

Problem Statement

Given a patient's clinical data (age, chest pain type, blood pressure, cholesterol, heart rate, ECG results, etc.), predict whether heart disease is present (1) or absent (0).

Dataset
Source: UCI Machine Learning Repository, Heart Disease, Cleveland Clinic Foundation (processed.cleveland.data)
Size: 303 patients, 13 features + 1 target
Target: the original num column (0 to 4) was converted to binary: 0 = no disease, 1 = disease (164 vs 139 patients, nearly balanced)
Missing values: ca (4) and thal (2), handled inside the pipeline
Why only Cleveland: the Hungarian, Switzerland and VA files have very high missing rates (for example ca missing in over 95% of rows)
Feature	Description
age	Age in years
sex	1 = male, 0 = female
cp	Chest pain type (1 to 4)
trestbps	Resting blood pressure (mm Hg)
chol	Serum cholesterol (mg/dl)
fbs	Fasting blood sugar > 120 mg/dl
restecg	Resting ECG result (0 to 2)
thalach	Maximum heart rate achieved
exang	Exercise induced angina
oldpeak	ST depression induced by exercise
slope	Slope of peak exercise ST segment
ca	Number of major vessels (0 to 3) coloured by fluoroscopy
thal	Thalassemia (3 normal, 6 fixed defect, 7 reversible defect)
Technologies

Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Joblib, Jupyter Notebook, Power BI

Project Structure
Heart-disease-classification/
├── data/
│   ├── raw/                  # original UCI files
│   └── processed/            # heart_clean.csv (used by Power BI)
├── notebooks/
│   └── heart_disease_analysis.ipynb
├── images/
│   ├── eda/                  # EDA and evaluation plots
│   └── dashboard/            # Power BI screenshots
├── models/
│   └── final_model.pkl
├── powerbi/
│   └── heart_dashboard.pbix
├── report/
├── requirements.txt
└── README.md
Methodology
Data cleaning: created the binary target, checked missing values, duplicates (none) and outliers (kept, since the values are medically plausible)
EDA: target distribution, age, chest pain type, max heart rate, sex and exercise angina vs target, correlation matrix
Preprocessing: 80/20 stratified train-test split; a scikit-learn Pipeline with median imputation + StandardScaler for numeric columns, mode imputation + OneHotEncoder for categorical columns. Everything is fitted on the training data only, to avoid data leakage
Models: Logistic Regression, Decision Tree (max_depth=4), Random Forest (200 trees)
Evaluation: accuracy, precision, recall, F1, ROC-AUC, confusion matrix and 5-fold cross-validation
Interpretation: permutation importance on the final model
Results
Model	Accuracy	Precision	Recall	F1	ROC-AUC
Logistic Regression	0.869	0.812	0.929	0.867	0.958
Decision Tree	0.787	0.742	0.821	0.780	0.860
Random Forest (final)	0.885	0.818	0.964	0.885	0.946

Final model: Random Forest, chosen for the highest Recall and F1. In a medical screening context, missing a patient who has the disease (false negative) is the costlier mistake, so Recall matters more than accuracy alone. Logistic Regression performed very closely.

Key findings

Patients with asymptomatic chest pain (cp = 4) show the highest disease rate (about 73%)
Lower maximum heart rate, exercise-induced angina and higher ST depression are associated with disease
Most important features for the model: ca, cp, thal, oldpeak
Feature importance shows what the model relies on. It does not prove that a feature causes heart disease
Dashboard


![Dashboard](images/dashboard/dashboard.png)
How to Run
bash
git clone <your-repo-url>
cd Heart-disease-classification
pip install -r requirements.txt
jupyter notebook notebooks/heart_disease_analysis.ipynb

Then run all cells (Kernel > Restart & Run All).

Limitations
Small dataset (303 patients) from a single hospital, so results may not generalise
The test set has only 61 rows, so metrics can vary between splits
Minimal hyperparameter tuning
Not validated for clinical use
Future Improvements
Hyperparameter tuning (GridSearchCV)
More models (XGBoost, SVM) and more data
Deploy as a Streamlit web app
Acknowledgement

Dataset creators: Andras Janosi (Hungarian Institute of Cardiology), William Steinbrunn (University Hospital, Zurich), Matthias Pfisterer (University Hospital, Basel), Robert Detrano (V.A. Medical Center, Long Beach and Cleveland Clinic Foundation).