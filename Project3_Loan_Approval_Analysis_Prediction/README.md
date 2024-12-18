# Loan Approval Prediction and Visualization

## Overview
This project aims to develop a machine learning model for predicting loan statuses based on various features of borrowers. The analysis involves data visualization, preprocessing, model training, evaluation, and hyperparameter tuning.

## Contents
1. **Data Visualization**
   - Histograms of numeric features.
   - Count plots for categorical features.
   - Boxplots for understanding distributions.
   
2. **Data Preprocessing**
   - Encoding categorical variables using `LabelEncoder`.
   - Scaling numeric features using `StandardScaler`.
   - Splitting the dataset into training and testing sets.

3. **Model Development**
   - Multiple classification models evaluated, including Logistic Regression, Random Forest, Gradient Boosting, XGBoost, and Support Vector Machine (SVM).
   - Performance metrics include confusion matrices, accuracy scores, and classification reports.

4. **Hyperparameter Tuning**
   - Used `GridSearchCV` and `Optuna` for optimizing the XGBoost model.

5. **Feature Importance and Model Interpretation**
   - Visualizations for model trees and feature importance.

6. **Cross-Validation**
   - Evaluating model stability and performance using k-fold cross-validation.

7. **Test Data Predictions**
   - Preprocessing test data and generating predictions for submission.

## Installation
To run this project, ensure you have the following libraries installed:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost optuna
```

## Data Visualization
### Numeric Features
Histograms with Kernel Density Estimation (KDE) are created for the following numeric features:
- `person_age`
- `person_income`
- `loan_amnt`
- `cb_person_cred_hist_length`

### Categorical Features
Count plots are generated for:
- `person_home_ownership`
- `loan_intent`
- `loan_grade`
- `cb_person_default_on_file`

### Boxplots
Boxplots are utilized to examine the distributions of numeric features across different loan statuses.

## Data Preprocessing
Categorical features are transformed into numerical values using `LabelEncoder`, and the numeric features are scaled for improved model performance.

## Model Development
The following models were trained and evaluated:
- **Logistic Regression**
- **Random Forest**
- **Gradient Boosting**
- **XGBoost**
- **Support Vector Machine (SVM)**

### Evaluation Metrics
Confusion matrices, accuracy scores, and classification reports provide insight into model performance.

## Hyperparameter Tuning
The best parameters for the XGBoost model were determined using both `GridSearchCV` and `Optuna`, resulting in improved accuracy.

## Feature Importance
The importance of each feature was visualized, helping to identify which features contribute most to model predictions.

## Cross-Validation
K-fold cross-validation was performed to assess the robustness of the final model, yielding a mean F1 score of approximately 0.814.

## Test Data Predictions
The trained model was applied to the test dataset, and predictions were saved for submission.

### Example Usage
To run the analysis:
1. Load your dataset and ensure it follows the expected structure.
2. Execute the preprocessing, model training, and evaluation steps.
3. Predict loan statuses for new data as shown in the code.

## Conclusion
This project demonstrates a comprehensive approach to building a loan status prediction model, covering essential steps from data exploration to model evaluation. Further improvements could include additional feature engineering and testing more advanced models.

## License
This project is licensed under the MIT License. Feel free to modify and use it according to your needs!
