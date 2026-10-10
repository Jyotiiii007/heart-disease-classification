# ❤️ Heart Disease Classification

A Machine Learning project that predicts the presence of heart disease using clinical patient data from the **Cleveland subset of the UCI Heart Disease Dataset**. The project covers data cleaning, exploratory data analysis (EDA), preprocessing, classification models, model evaluation, feature importance, and an interactive Power BI dashboard.

> **Disclaimer:** This project is developed for educational purposes only. It is not intended for medical diagnosis or clinical decision-making.

## 📌 Project Overview

Heart disease is a major health concern, and analyzing clinical data can help identify patterns associated with its presence. This project uses machine learning techniques to classify patients based on medical attributes such as age, chest pain type, resting blood pressure, cholesterol, maximum heart rate, and exercise-induced angina.

The primary objective is to build and compare classification models and understand how different clinical features contribute to their predictions.

## 🎯 Problem Statement

Given a patient's clinical measurements, predict whether heart disease is present or absent.

- **0 — No heart disease**
- **1 — Heart disease present**

The project also compares model performance using multiple evaluation metrics, with particular attention to recall because false negatives can be important in a screening context.

## 📊 Dataset

- **Source:** UCI Machine Learning Repository — Heart Disease Dataset
- **Subset:** Cleveland
- **Original file:** `processed.cleveland.data`
- **Total records:** 303 patients
- **Input features:** 13
- **Target variable:** Binary classification label derived from the original `num` column

The original target contains values from 0 to 4. It was converted into a binary target, where 0 represents no disease and values 1–4 represent the presence of disease.

| Target | Number of patients |
|---|---:|
| No heart disease (0) | 164 |
| Heart disease present (1) | 139 |

Missing values in the `ca` and `thal` columns were handled through the preprocessing pipeline.

**Why the Cleveland subset?**

The project uses the Cleveland dataset because it provides a manageable dataset for a beginner-friendly classification workflow. Other subsets have substantial missing data, which would require additional investigation and preprocessing.

## 🧾 Features Used

| Feature | Description |
|---|---|
| `age` | Patient's age in years |
| `sex` | Sex (1 = male, 0 = female) |
| `cp` | Chest pain type |
| `trestbps` | Resting blood pressure |
| `chol` | Serum cholesterol level |
| `fbs` | Whether fasting blood sugar is greater than 120 mg/dl |
| `restecg` | Resting electrocardiographic results |
| `thalach` | Maximum heart rate achieved |
| `exang` | Exercise-induced angina |
| `oldpeak` | ST depression induced by exercise |
| `slope` | Slope of the peak exercise ST segment |
| `ca` | Number of major vessels visualized by fluoroscopy |
| `thal` | Thalassemia-related test category |

## 🛠️ Technologies Used

- **Programming:** Python
- **Data manipulation:** Pandas, NumPy
- **Data visualization:** Matplotlib, Seaborn
- **Machine learning:** Scikit-learn
- **Model persistence:** Joblib
- **Development environment:** Jupyter Notebook
- **Dashboard and reporting:** Microsoft Power BI

## 🔄 Project Workflow

### 1. Data Cleaning and Preparation
- Loaded and inspected the dataset.
- Converted the original target into a binary classification label.
- Checked for missing values and duplicate records.
- Examined potential outliers and retained values considered medically plausible.
- Prepared the cleaned dataset for analysis and visualization.

### 2. Exploratory Data Analysis (EDA)

Explored the relationship between clinical features and heart disease using:

- Target class distribution
- Age distribution
- Chest pain type and heart disease
- Maximum heart rate and heart disease
- Sex and heart disease
- Exercise-induced angina and heart disease
- Correlation matrix

### 3. Data Preprocessing

- Split the data into training and testing sets using an 80:20 ratio.
- Used stratified sampling to preserve the target class distribution.
- Applied median imputation and standardization to numerical features.
- Applied mode imputation and one-hot encoding to categorical features.
- Used a Scikit-learn Pipeline and fitted preprocessing steps on the training data to reduce data leakage.

### 4. Model Training

Three classification algorithms were implemented and compared:

1. **Logistic Regression** — a baseline classification model.
2. **Decision Tree** — a tree-based model with `max_depth=4`.
3. **Random Forest** — an ensemble model using 200 trees.

### 5. Model Evaluation

Models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion matrix
- 5-fold cross-validation

### 6. Feature Importance

Permutation importance was used to investigate which features most influenced the final model's predictions.

Feature importance describes the model's reliance on features; it does not establish causation.

### 7. Power BI Dashboard

An interactive dashboard was developed to present key findings and make the dataset easier to explore visually.

The cleaned dataset is available for dashboard development in `data/processed/heart_clean.csv`.

## 📈 Model Performance

The following results were obtained from the project evaluation.

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 86.9% | 81.2% | 92.9% | 86.7% | 95.8% |
| Decision Tree | 78.7% | 74.2% | 82.1% | 78.0% | 86.0% |
| Random Forest | **88.5%** | **81.8%** | **96.4%** | **88.5%** | 94.6% |

*Note: These are the recorded project results. Actual performance can vary depending on the train-test split and experimental setup.*

### 🏆 Final Model: Random Forest

Random Forest was selected as the final model because it achieved the highest accuracy, recall, and F1-score among the three evaluated models.

Its recall of 96.4% indicates that it identified a high proportion of positive cases in the evaluated test set. Recall is particularly relevant when examining false negatives in a screening-oriented classification task.

Logistic Regression also performed well and achieved the highest ROC-AUC in this comparison. Therefore, model selection depends on the evaluation metric and intended use rather than accuracy alone.

## 🔍 Key Findings

- Patients with asymptomatic chest pain (`cp = 4`) showed the highest disease rate in the analyzed dataset, at approximately 73%.
- Lower maximum heart rate was associated with a higher prevalence of heart disease in the dataset.
- Exercise-induced angina and higher ST depression values were associated with heart disease.
- The leading features identified through permutation importance included `ca`, `cp`, `thal`, and `oldpeak`.

These findings describe patterns in this dataset and should not be interpreted as medical conclusions or evidence of causation.

## 📊 Dashboard Preview

![Heart Disease Power BI Dashboard](images/dashboard/dashboard.png)

The Power BI dashboard presents selected patient statistics and visual comparisons to support exploratory analysis.

## 📁 Project Structure

```text
Heart-disease-classification/
├── data/
│   ├── raw/                 # Original dataset files
│   └── processed/           # Cleaned dataset for analysis and Power BI
├── notebooks/
│   └── heart_disease_analysis.ipynb
├── images/
│   ├── eda/                 # EDA and model evaluation plots
│   └── dashboard/           # Dashboard screenshots
├── models/
│   └── final_model.pkl
├── powerbi/
│   └── heart_dashboard.pbix
├── report/                  # Project report
├── requirements.txt
└── README.md
```

## 🚀 How to Run the Project

### Prerequisites

Install Python and Git. Jupyter Notebook is used to run the analysis.

### Step 1: Clone the repository

```bash
git clone <your-repository-url>
cd Heart-disease-classification
```

### Step 2: Install dependencies

```bash
pip install -r requirements.txt
```

### Step 3: Open Jupyter Notebook

```bash
jupyter notebook notebooks/heart_disease_analysis.ipynb
```

Restart the kernel and run all cells to reproduce the analysis, model training, and evaluation.

**Note:** Ensure the raw dataset is available at the path expected by the notebook. The Power BI dashboard requires the cleaned CSV file and may need its data source path updated on another computer.

## ⚠️ Limitations

- The dataset contains only 303 patients from the Cleveland subset.
- The data comes from a limited clinical setting and may not represent other populations.
- The test set contains approximately 61 patients, so evaluation metrics may vary.
- Extensive hyperparameter tuning has not been performed.
- The results have not been independently validated for clinical use.
- The model should not be used to diagnose or guide the treatment of any patient.

## 🔮 Future Improvements

- Perform hyperparameter tuning using `GridSearchCV`.
- Evaluate additional algorithms, such as Support Vector Machines and XGBoost.
- Validate performance using additional datasets and more robust evaluation strategies.
- Improve the Power BI dashboard with additional interactive filters and insights.
- Develop a Streamlit application to demonstrate the model's predictions for educational purposes.

## 🙏 Acknowledgements

The Heart Disease Dataset is associated with the following contributors and institutions:

- Andras Janosi — Hungarian Institute of Cardiology
- William Steinbrunn — University Hospital, Zurich
- Matthias Pfisterer — University Hospital, Basel
- Robert Detrano — V.A. Medical Center, Long Beach, and Cleveland Clinic Foundation

**Dataset source:** UCI Machine Learning Repository — Heart Disease Dataset.


*Developed as a learning project to practice data analysis, machine learning, model evaluation, and data visualization.*
