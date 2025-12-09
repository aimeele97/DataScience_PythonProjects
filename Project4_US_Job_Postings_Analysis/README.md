# **Data Science Job Salary Analysis & Prediction**

*Exploring trends, cleaning messy job-posting data, and predicting salaries using CatBoost*

![image.png](img/indeedlogo.png)

---

# ** Project Overview**

The data science job market is competitive, fast-changing, and often difficult to interpret. To make sense of hiring patterns and compensation trends, I analyzed a dataset of U.S. data science job postings collected from Kaggle.


This end-to-end project includes:

1. **Automated Data Cleaning** – turning raw web-scraped postings into structured features
2. **Exploratory Data Analysis (EDA)** – uncovering hiring, location, salary, skill, and seniority trends
3. **Predictive Modeling** – using **CatBoost** to analyze feature importance and reveal which job attributes most strongly influence salary.

---

# **1. Data Preparation & Cleaning (What I Did, Why It Matters)**

The raw dataset was **messy**, inconsistent, and incomplete — containing mixed salary formats, embedded metadata in titles, unstructured locations, and missing fields.  

To fix this, I built a **modular cleaning pipeline** (full notebook: [Cleansing Script](p1-automate_script_clean.ipynb)) that transforms raw text into reliable features.

### ✔ 1.1. Deduplication & Standardization

* Dropped duplicate rows
* Replaced blank values with NaN
* Removed irrelevant fields (e.g., job URLs)

👉 **Outcome:** A clean, consistent foundation for grouping, modeling, and aggregation.

---

### ✔ 1.2. Standardized Company & Title Text

* Applied capitalization
* Normalized naming to avoid inconsistencies (e.g., "google", “GOOGLE”, “Google”)

👉 **Outcome:** Companies and roles became properly grouped, improving insights and reducing noise.

---

### ✔ 1.3. Extracted Job Level & Work Mode from the Title

Job titles often secretly encode information, such as:

* **Work mode:** remote, hybrid, on-site
* **Level:** senior, junior, associate, manager, lead

The cleaning pipeline automatically detects these and creates two new features:
**`Work Mode`** and **`Level`**.

👉 **Outcome:** Revealed market structure — mid-level jobs heavily dominate while entry-level roles are rare.

---

### ✔ 1.4. Cleaned and Split Location Data

The raw location strings were inconsistent (“Austin, TX 78701”, “Remote in US”, “San Francisco, CA 94103”).
The pipeline:

* Extracted **City** and **State**
* Normalized remote cities to “Remote”
* Removed misleading “in …” suffixes
* Cleaned postal codes

👉 **Outcome:** Accurate location segmentation and clean geographic analysis.

---

### ✔ 1.5. Advanced Salary Extraction

This was the most complex part of cleaning.

Salary fields contained:

* Ranges (`$90k–$120k`)
* Hourly/day/monthly/yearly formats
* “shift” emails mistakenly tagged as salary
* Missing salaries only found in descriptions
* Fake integers from schedule codes (e.g., “9x80”)
* Values like (`120k`) or (`$150,000`)

The pipeline handled this by:

1. Extracting digits & ranges
2. Using description text to fill missing salaries
3. Removing false positives
4. Identifying **Pay Type** (hour, day, week, month, year)
5. Converting everything to **annual salary**
6. Calculating reliable **Average Salary**
7. Manually correcting anomalies (e.g., L3Harris “9x80” case)

👉 **Outcome:** A usable, numeric salary field — essential for modeling.

---

### ✔ 1.6. Final Cleaning Output

After cleaning, these columns were retained:

* **Date**, **Title**, **Company**, **State**, **City**
* **Level**, **Work Mode**
* **Average Salary**, **Pay Type**, **Employment Type**
* **Description**

📄 **Cleaned dataset:** [completed_file.csv](completed_file.csv)

---

# **2. Exploratory Data Analysis (EDA)**

Full EDA notebook: [EDA & Modeling Notebook](p2-eda_modeling.ipynb)

### ⭐ Geography & Hiring Trends

* **California** dominates job postings, driven by tech hubs
* Most roles are **full-time (~97%)**
* **Mid-level and senior** roles make up the majority
* Entry-level and managerial positions are uncommon

### ⭐ Salary Insights

* Median annual salary ~**$157K**
* Salaries cluster below the median because of many mid-level roles
* Certain companies (Amazon, Meta, etc.) pay much higher — mostly for senior or specialized roles

### ⭐ Job Levels & Work Types

* Entry-level roles represent **less than 1%**
* Senior / Staff / Lead roles are heavily represented
* Work mode is often missing, but remote roles show clear clustering by industry

### ⭐ Skill Analysis

Most frequently mentioned skills include:

* **Machine Learning**
* **Artificial Intelligence**
* **Deep Learning**
* **R**

Python, SQL, AWS, and Tableau appear less often in text, likely because many employers describe capabilities rather than listing tools.

**Interactive Dashboard**:
👉 [Tableau Job Posting Dashboard](https://public.tableau.com/app/profile/aimee.le9707/viz/job_posting_17304216955380/Dashboard1)

---

# **3. Predictive Modeling: CatBoost Regressor**

### **Target:** Annual Salary

### **Features included:**

* Title + Level
* Company
* State & City
* Skills (extracted from descriptions)
* Employment Type
* Work Mode

CatBoost efficiently handled categorical data using built-in encodings and achieved:

### **Performance**

* **Training R²:** 0.70
* **Validation R²:** 0.58
* Mild overfitting but strong generalization
* Captures salary *patterns*, not exact values

### Feature Importance

| Feature             | Importance | Meaning                                                  |
| ------------------- | ---------- | -------------------------------------------------------- |
| **Company**         | 39%        | Employer identity is the strongest salary determinant    |
| **Title + Level**   | 21%        | Seniority and specialization significantly influence pay |
| **State**           | 16%        | Regional differences matter (e.g., CA vs Midwest)        |
| **City**            | 12%        | Urban hubs drive higher compensation                     |
| **Employment Type** | 8%         | Full-time vs contract influences salary range            |
| **Skills**          | 4%         | Skill lists matter but have far less impact              |

### Interpretation

The model reflects reality:
💼 **Who you work for** and **what level you're at** matter more than any skill you list.

---

# **Predicted Salaries**

The model can predict annual salary given:

* Job title + seniority
* Company
* State / City
* Description keywords

Predictions follow macro trends and are useful for salary benchmarking — not exact compensation levels.

---

# **Recommendations & Next Steps**

1. **Enhance the model** with:

   * Experience years
   * Work mode
   * Education level
   * Industry sector
2. Apply **hyperparameter tuning** (Optuna / GridSearch)
3. Try **stacking CatBoost + LightGBM + XGBoost**
4. Use **cross-validation** for stronger generalization
5. Visualize salary bands rather than exact predictions for clarity

---

# **Tools & Libraries**

* **pandas**, **numpy**
* **matplotlib**, **seaborn**, **wordcloud**
* **catboost**, **scikit-learn**

---

# **Final Takeaways**

* Salary differences are primarily driven by **company** and **job level**
* Location plays an important but secondary role
* Skill lists influence salary less than expected
* CatBoost predictions provide realistic salary trend estimates
* Data science roles are concentrated in tech-heavy states and mid-senior levels

