# Data Science Job Salary Analysis & Prediction

![image.png](img/indeedlogo.png)

---

## **Project Overview**

This project analyzes **US Data Scientist job postings** collected over two months to uncover salary trends and predict expected salaries for different job profiles.

The workflow includes:

1. **Data Cleaning** – Handling raw scraped data and preparing it for analysis.
2. **Exploratory Data Analysis (EDA)** – Exploring patterns in hiring, locations, job levels, salaries, and skills.
3. **Predictive Modeling** – Using **CatBoost Regressor** to model and predict annual salaries based on job profile features.

**Key Insights for Stakeholders:**

* **Company** and **job level** drive the majority of salary differences.
* **California** dominates hiring, particularly for mid-level and senior roles.
* Predicted salaries capture **trends**, not exact values—actual pay may vary due to negotiation or unique responsibilities.

---

## **Data Source**

The dataset was collected from Kaggle and contains US Data Scientist job postings for approximately two months.

* **Raw dataset:** [Raw Data (CSV)](indeed_kaggle.csv)

---

## **Data Preparation & Cleaning**

The scraped dataset was **raw and unstructured**, requiring preprocessing before analysis.

* Steps included:

  * Handling missing values and inconsistent formatting
  * Creating new columns such as:

    * **`Title_level`**: combination of job title and level
    * **Skill keywords**
  * Encoding categorical fields for modeling

- **Data cleansing code:** [Cleansing Script](p1-automate_script_clean.ipynb)
- **Cleaned dataset:** [Cleaned Dataset](completed_file.csv)

---

## **Exploratory Data Analysis (EDA)**

### **1. Geography & Hiring Trends**

* **California** dominates hiring, driven by tech hubs like Silicon Valley.
* Most roles are **full-time (~97%)**.
* **Mid-level and senior positions** are most common; low-level and manager roles are rare.

### **2. Salary Insights**

* Most salaries are below the **median $157K**, representing typical market ranges.
* Certain companies (e.g., Amazon) pay significantly higher, likely due to **seniority or special responsibilities**.

### **3. Job Levels & Employment Type**

* Entry-level and managerial positions are relatively uncommon.
* Full-time roles dominate; contract or part-time roles are limited.

**Visualizations Used:** histograms, boxplots, word clouds to explore distributions and patterns.

---

## **Modeling: CatBoost Regressor**

* **Target Variable:** `Annual Salary`
* **Features:** `Title_level`, `Company`, `State`, `City`, `Employment Type`, `Skill keywords`
* **Approach:** Categorical and text features handled using **CatBoost Pools**

**Performance Metrics:**

* **Training R²:** 0.70 → explains 70% of variance in training data
* **Validation R²:** 0.58 → explains 58% of variance in unseen data
* **Slight overfitting**, but model generalizes reasonably well

**Interpretation:** The model captures **overall salary trends**; individual salaries may vary due to negotiation, experience, or unobserved factors.

* **EDA and modeling code:** [EDA & Modeling Notebook](p2-eda_modeling.ipynb)
* **Interactive Dashboard (Tableau):** [Job Postings Dashboard](https://public.tableau.com/app/profile/aimee.le9707/viz/job_posting_17304216955380/Dashboard1)

---

## **Feature Importance**

| Feature         | Importance | Interpretation                                     |
| --------------- | ---------- | -------------------------------------------------- |
| Company         | 39%        | Employer has the largest impact on salary          |
| Title + Level   | 21%        | Seniority and role type strongly affect pay        |
| State           | 16%        | Regional differences influence pay                 |
| City            | 12%        | Location within state also matters                 |
| Employment Type | 8%         | Full-time vs contract or part-time affects salary  |
| Skills          | 4%         | Specific skills have smaller but measurable effect |

**Stakeholder Takeaway:** Salary differences are mostly driven by **company and job level**, followed by location, while skills and employment type are less influential.

---

## **Predicted Salaries**

* Model predicts **expected salary** for a given job profile.
* Example: A Senior Engineer at Company X in New York receives an estimate aligned with typical market trends.
* Predictions **capture trends**, not exact figures—individual salaries may differ due to negotiation or hidden factors.

---

## **Recommendations & Next Steps**

1. Use predicted salaries for **budgeting, benchmarking, and market trend insights**.
2. Enhance features by including **experience, education, work mode, or certifications** to improve accuracy.
3. Conduct **hyperparameter tuning** using GridSearchCV or Optuna.
4. Combine CatBoost with **LightGBM or XGBoost** in stacked models for better performance.
5. Use **K-Fold cross-validation** for robust validation and reduced variance in R².
6. Communicate results using **salary ranges or bins** instead of exact predictions for clarity.

---

## **Tools & Libraries**

* **Data Manipulation & Analysis:** `pandas`, `numpy`, `collections.Counter`
* **Visualization:** `matplotlib`, `seaborn`, `wordcloud`
* **Modeling:** `catboost`, `scikit-learn`

---

## **Key Takeaways**

* **Company** and **job level** are the primary drivers of salary differences.
* **Location** also influences pay, but skills and employment type have smaller impact.
* Predictions are **trend indicators** rather than precise figures.
* Improving model performance requires **more relevant features** to capture hidden factors such as negotiation, responsibilities, and experience.
