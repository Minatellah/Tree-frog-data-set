# Model Stacking for Regression Using Tidymodels

## Overview

This project explores **stacked ensemble learning** for a regression task using the **tidymodels** and **stacks** frameworks in R.  
The objective is to improve predictive performance by combining multiple base learners through a stacking approach, rather than relying on a single model.

The analysis is conducted on the *tree_frogs* dataset, with **latency** as the response variable.

---

## Dataset Preparation

The dataset was first cleaned by removing observations with missing values in the response variable (`latency`).  
An exploratory analysis was conducted to examine the relationship between latency, age, and treatment groups, revealing variability that motivates the use of flexible, non-linear models alongside simpler linear approaches.

The data was then split into training and testing sets, with stratification on the response variable to preserve its distribution across splits.

---

## Cross-Validation and Evaluation Metric

Model evaluation was based on **root mean squared error (RMSE)**, which is appropriate for continuous outcomes and penalizes large prediction errors.

To ensure robust performance estimation, **5-fold cross-validation** was applied to the training data.  
This resampling strategy was used consistently across all candidate models to ensure fair comparison and reliable stacking.

---

## Base Learners

Three different regression models were considered as base learners, each capturing different structural assumptions:

- **k-Nearest Neighbors (kNN)**  
  A non-parametric method capable of modeling complex, local patterns in the data.

- **Linear Regression**  
  A baseline model providing interpretability and capturing linear relationships.

- **Support Vector Machine with Radial Basis Function Kernel (SVM-RBF)**  
  A flexible model capable of capturing non-linear relationships through kernel methods.

Each model was paired with an appropriate preprocessing recipe, including steps such as:
- Encoding categorical predictors
- Removing zero-variance predictors
- Imputing missing numeric values
- Normalizing numeric features
- Reducing multicollinearity when necessary

---

## Hyperparameter Tuning

For models requiring hyperparameter selection (kNN and SVM), tuning was performed using grid search within the cross-validation framework.  
All candidate models were evaluated using the same resampling strategy and performance metric to ensure comparability.

---

## Stacking Procedure

The stacking process was implemented using the **stacks** package:

1. Candidate models were added to the stack using their resampling results.
2. Predictions from all candidate models were blended using regularized linear regression.
3. A penalty parameter was applied to control model complexity and prevent overfitting.
4. Only models contributing positively to performance were retained in the final ensemble.

The resulting stack assigns different weights to the base learners, reflecting their relative contribution to predictive accuracy.

---

## Final Model and Evaluation

The selected ensemble model was trained on the full training dataset and evaluated on the held-out test set.

Predicted values were compared to observed latency values, and diagnostic plots confirmed good agreement between predictions and actual outcomes.  
The stacked model demonstrated improved performance and stability compared to individual base learners.

---

## Conclusion

This project illustrates the effectiveness of **model stacking** as a principled ensemble learning strategy.  
By combining models with complementary strengths, stacking allows for improved predictive accuracy and robustness while maintaining a systematic and reproducible workflow.

The use of the tidymodels ecosystem ensures clarity, modularity, and statistical rigor throughout the modeling process.

---

---
