# IBM-employee-attrition-prediction-ml
Predicted IBM employee attrition using Logistic Regression and Random Forest models. Performed data preprocessing, feature engineering, EDA, and model evaluation. Achieved 89.8% accuracy with Logistic Regression and identified key factors influencing employee turnover to support workforce planning and retention strategies.

# IBM Employee Attrition Prediction Using Machine Learning

## 📌 Project Overview

Employee attrition can significantly impact an organization through increased hiring costs, loss of experienced employees, and reduced productivity. This project uses machine learning to predict whether an employee is likely to leave or remain with a company based on demographic, compensation, job-related, and workplace factors.

Using the IBM HR Analytics Employee Attrition & Performance dataset, I developed and compared Logistic Regression and Random Forest classification models and analyzed the factors associated with employee turnover.

---

## 🎯 Project Objective

The primary objectives of this project were to:

- Predict whether an employee is likely to leave the company.
- Compare the predictive performance of Logistic Regression and Random Forest.
- Identify important factors associated with employee attrition.
- Translate model findings into meaningful business insights that could support employee retention strategies.

---

## 📊 Dataset

The project uses the **IBM HR Analytics Employee Attrition & Performance** dataset.

The dataset contains **1,470 employee records** with variables related to:

- Age
- Monthly Income
- Overtime
- Business Travel
- Job Satisfaction
- Work-Life Balance
- Distance From Home
- Job Role
- Years at Company
- Training
- Attrition status

**Target Variable:** `Attrition`

The target represents whether an employee left the organization (`Yes`) or remained with the organization (`No`).

---

## 🛠️ Technologies & Tools

- **R**
- **R Markdown**
- **caret**
- **randomForest**
- **ggplot2**
- Logistic Regression
- Random Forest
- Classification & Predictive Modeling
- Confusion Matrix Evaluation

---

## 🔄 Project Workflow

### 1. Data Understanding
- Examined the dataset structure and summary statistics.
- Checked the dataset for missing values.

### 2. Data Preprocessing
- Converted the Attrition target variable into binary format.
- Removed variables not useful for prediction.
- Converted categorical variables into factors.
- Split the dataset into **80% training data and 20% testing data**.

### 3. Model Development

Two classification models were developed:

**Logistic Regression**
- Estimated the probability of employee attrition.
- Converted predicted probabilities into employee leave/stay classifications.

**Random Forest**
- Built an ensemble classification model for attrition prediction.
- Used variable importance to investigate influential predictors.

### 4. Model Evaluation

Both models were evaluated on unseen testing data using confusion matrices and classification performance metrics.

---

## 📈 Model Results

| Model | Accuracy |
|---|---:|
| Logistic Regression | **89.8%** |
| Random Forest | **85.7%** |

Logistic Regression achieved the highest overall accuracy at **89.8%**, compared with **85.7%** for Random Forest.

---

## 🔍 Key Findings

The analysis identified several factors associated with employee attrition, including:

- Overtime
- Business Travel
- Distance From Home
- Job Satisfaction
- Work-Life Balance
- Monthly Income
- Years Since Last Promotion
- Number of Companies Worked

Random Forest variable importance also highlighted **Monthly Income, Age, Total Working Years, Job Role, Overtime, and Distance From Home** as influential variables.

---

## 💼 Business Impact

The results demonstrate how predictive analytics can be used to support workforce planning and employee retention.

Organizations could use insights from employee attrition models to:

- Identify workforce groups with higher attrition risk.
- Investigate excessive overtime and workload.
- Improve work-life balance initiatives.
- Review compensation and promotion opportunities.
- Develop targeted employee engagement and retention strategies.
