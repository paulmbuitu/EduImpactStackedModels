# 📊 Evaluating the Impact of School Environment on Student Academic Success

## 📌 Overview

This project investigates how internal school-level environmental factors—those within a school's control—correlate with student academic success, distinct from broader socioeconomic variables. Using data from New York City public elementary schools across the 2018–2019 and 2019–2020 academic years, we analyze how elements such as teacher collaboration, leadership, and supportive environments influence mathematics test scores.

---

## 🎯 Objective

- **Primary Goal:**  
  Evaluate the extent to which the school environment affects academic success, independently of students’ socioeconomic backgrounds.

- **Sub-Goal:**  
  Identify the most impactful components of the school environment contributing to student performance.

---

## 📂 Data Sources

All datasets are sourced from the [NYC Open Data portal](https://opendata.cityofnewyork.us/) and the NYC Department of Education. The analysis focuses on:

- **Demographic Snapshot (2017–2022):**  
  Student enrollment by grade, ethnicity, gender, disability status, and economic indicators.

- **Math Test Results (2013–2023):**  
  School-level performance on state mathematics exams, categorized into four performance tiers.

- **NYC School Surveys (2017–2020):**  
  Annual feedback from students, parents, and teachers, covering six core school environment elements:
  - Rigorous Instruction  
  - Collaborative Teachers  
  - Supportive Environment  
  - Effective School Leadership  
  - Strong Family-Community Ties  
  - Trust

**Note:** The analysis excludes the 2017–2018 academic year due to inconsistencies in math exam scoring, and 2020–2021 due to COVID-19 disruptions.

---

## 🧪 Methodology

### 🔧 Data Processing

- Merged data across multiple years and datasets  
- Focused on 475 NYC elementary schools  
- Handled missing data and transformed relevant categorical variables  
- Isolated environmental factors from socioeconomic indicators for clarity  

### 📉 Statistical Modeling

#### 1. **Ordinary Least Squares (OLS) Regression**  
Initial baseline model to evaluate linear relationships and validate assumptions.

#### 2. **Ensemble Stacking for Regression**  
Two models were tested using Ridge Regression as the meta-learner:

| Model Stack                        | RMSE  | MAE   | R²    | Accuracy |
|-----------------------------------|-------|-------|-------|----------|
| RF + GB + Linear Regression       | 0.443 | 0.214 | 0.758 | 86.8%    |
| **RF + GB + KNN (Selected Model)**| **0.101** | **0.073** | **0.977** | **96.6%**  |

> 💡 The addition of KNN captured local relationships and significantly boosted prediction accuracy.

#### 3. **Ensemble Stacking for Classification**  
Used for predicting performance tiers:

- **Base Models:** XGBoost + LightGBM  
- **Meta-Learner:** Logistic Regression  

| Metric     | Score   |
|------------|---------|
| Accuracy   | 93.7%   |
| Macro F1   | 91.9%   |

---

## 🏆 Final Model Selections

- **Best Regression Model:** RF + GB + KNN Stacked Regressor  
- **Best Classification Model:** Logistic Regression + XGBoost + LightGBM  

These models demonstrate high accuracy and generalizability, effectively identifying relationships between school environment quality and academic outcomes.

---

## 🧠 Key Insights

- School environment factors can explain a significant portion (~98%) of student performance variance.  
- “Supportive Environment” and “Collaborative Teachers” showed especially strong correlations with math performance.  
- Ensemble models that combine global and local learning perspectives (e.g., GB, RF, KNN) outperform single-model baselines.

---

## 🚀 Usage

To run the notebook:

1. Clone the repository or download the notebook.  
2. Ensure you have Python 3.x with packages listed in `requirements.txt` (e.g., `pandas`, `numpy`, `scikit-learn`, `xgboost`, `lightgbm`, `matplotlib`, `seaborn`).  
3. Run all cells in order for end-to-end data processing, modeling, and evaluation.

---

## 📎 Limitations

- Limited time range (2018–2020) due to data consistency and pandemic impact.  
- Results may not generalize beyond NYC public elementary schools.

---

## 📘 Acknowledgments

Data provided by NYC Department of Education and NYC Open Data.
