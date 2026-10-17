# IBM Employee Attrition Prediction (R, Machine Learning)

**In one line:** I built and compared two machine learning models in R that predict whether an employee will leave a company, and I used them to find the factors most linked to employee turnover.

---

## The problem

Losing employees is expensive. Every departure means hiring and training costs, lost experience, and slower teams. If HR can see early which employees are most likely to leave and why, they can step in before it happens. This project asks two questions:

1. Can we predict which employees are likely to leave?
2. Which factors are most strongly linked to leaving?

## What I did

1. **Explored the data.** I reviewed 1,470 employee records and confirmed that no values were missing.
2. **Cleaned it up.** I turned the "left / stayed" outcome into a 1/0 target, removed four columns that carry no information (`EmployeeCount`, `Over18`, `StandardHours`, `EmployeeNumber`), and converted text columns into categories.
3. **Held data back for testing.** I trained the models on 80% of the employees (1,176) and tested them on the other 20% (294), which the models never saw during training.
4. **Built two models.** The first is Logistic Regression, a simple model whose results are easy to explain. The second is Random Forest, a more complex model that combines many decision trees.
5. **Evaluated and interpreted them.** I compared the models using confusion matrices and then looked at which factors drove their predictions.

## Key results

The test set has 294 employees: 246 stayed and 48 left.

| Metric (test set, 294 employees) | Logistic Regression | Random Forest |
|---|---:|---:|
| **Accuracy** | **89.8%** | 85.7% |
| Leavers correctly identified (recall) | **24 of 48 (50.0%)** | 8 of 48 (16.7%) |
| Stayers correctly identified | 240 of 246 (97.6%) | 244 of 246 (99.2%) |
| Precision when predicting "will leave" | 80.0% | 80.0% |
| Balanced accuracy | 73.8% | 57.9% |
| Kappa | 0.56 | 0.23 |

**Logistic Regression was the better model.** It caught three times as many actual leavers as Random Forest.

**A note on class imbalance:** only about 16% of employees in the data left (237 of 1,470). A model that simply predicted "everyone stays" would already score **83.7% accuracy**, so accuracy alone overstates performance. The more meaningful number is that Logistic Regression correctly flagged **half of the employees who actually left**. Random Forest's accuracy was not statistically better than that "everyone stays" baseline (p = 0.19).

## What the model found

**Factors linked to a *higher* chance of leaving** (statistically significant in the Logistic Regression model, p < 0.05):

- Working **overtime**. This was the strongest and most significant factor.
- **Frequent business travel**
- Being **single** (compared with married)
- Having worked at **more previous companies**
- More **years since the last promotion**
- A longer **commute** (distance from home)
- Working in the **Laboratory Technician** role

**Factors linked to a *lower* chance of leaving:**

- Higher **job satisfaction** and **environment satisfaction**
- Higher **job involvement**
- Better **work-life balance**
- Better **relationship satisfaction** at work
- Being **older**, and having spent more **years in the current role**
- More **training sessions** in the past year

**Random Forest's most important variables** were Monthly Income, Age, Total Working Years, Daily Rate, Monthly Rate, Job Role, and Overtime. Importance scores show how much each variable helped the predictions, but not whether it pushes attrition up or down.

> These are associations in the data, not proof of cause and effect.

## Business recommendations

The findings above suggest a few areas an HR team might look into. These are starting points, not tested interventions:

- **Monitor and manage overtime.** It was the strongest signal of leaving.
- **Review travel demands** for roles with frequent travel.
- **Check promotion timelines** for employees who have gone a long time without one.
- **Track satisfaction and engagement** (job, environment, involvement, work-life balance) as early warning signs.
- **Consider flexible or hybrid options** where long commutes are common.
- **Use the model as a screening aid**, not an automatic decision tool. It still misses about half of leavers.

## Tools & methods

| Area | What I used |
|---|---|
| Language | R, R Markdown |
| Data split | `caret::createDataPartition` (80/20, `set.seed(123)`) |
| Models | Logistic Regression (`glm`, binomial), Random Forest (`randomForest`, 500 trees) |
| Evaluation | `caret::confusionMatrix` (accuracy, sensitivity, specificity, kappa) |
| Interpretation | Logistic Regression coefficients, `caret::varImp` for Random Forest |

## Repository structure

```
├── code/
│   └── Employee_Attrition_Prediction.Rmd   # Full analysis (R Markdown)
├── data/
│   └── WA_Fn-UseC_-HR-Employee-Attrition.csv  # IBM HR Analytics dataset (1,470 rows, 35 columns)
├── report/
│   └── ML_Final_Project_Report_.pdf        # Written project report
└── README.md
```

## How to reproduce

1. Install R and these packages:
   ```r
   install.packages(c("caret", "randomForest", "rmarkdown"))
   ```
2. Clone the repository:
   ```bash
   git clone https://github.com/rajvi669/IBM-employee-attrition-prediction-ml.git
   ```
3. The R Markdown file reads `WA_Fn-UseC_-HR-Employee-Attrition.csv` from its own folder. Copy the file from `data/` into `code/`, or change the path in the `read.csv()` line to `"../data/WA_Fn-UseC_-HR-Employee-Attrition.csv"`.
4. Open `code/Employee_Attrition_Prediction.Rmd` in RStudio and click **Knit**, or run every chunk in order. With `set.seed(123)`, you should get the results shown above.

## About the dataset

- **Source:** IBM HR Analytics Employee Attrition & Performance (available on Kaggle)
- **Size:** 1,470 employees and 35 columns, with no missing values
- **Outcome:** `Attrition` (Yes/No). 237 employees left (16.1%) and 1,233 stayed.
- **Important:** this is a **fictional dataset created by IBM data scientists** for teaching and practice. It does not describe real employees at IBM or any other company, so the findings show the method working, not real-world workforce facts.

## Limitations & next steps

**Limitations**

- **Class imbalance.** With only 16% leavers, both models lean toward predicting "stays." Logistic Regression still misses half of leavers.
- **Default settings.** Both models use a fixed 0.5 probability cutoff (Logistic Regression) or default parameters (Random Forest), with no tuning.
- **One train/test split.** The results come from a single 294-employee test set, so they could shift with a different split.
- **Fictional data.** The findings may not carry over to a real organization.

**Next steps**

- Handle the imbalance with class weights, up- or down-sampling, or SMOTE, and tune the probability cutoff to catch more leavers.
- Report ROC-AUC and precision-recall curves, and use k-fold cross-validation.
- Tune Random Forest (`mtry`, number of trees) and try gradient boosting (e.g., XGBoost).
- Add explainability for individual predictions (e.g., SHAP).

## Author

**Rajvi Soni**, MS Business Analytics, Kent State University
LinkedIn: [linkedin.com/in/sonirajvi18](https://www.linkedin.com/in/sonirajvi18)
