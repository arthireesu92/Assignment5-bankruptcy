Assignment 5 – Bankruptcy Prediction using XGBoost

Student:** Arthi Reesu

🔷 1. Project Overview

This project focuses on building a **binary classification model** to predict whether a company is likely to go bankrupt based on financial indicators. The goal is not only to produce a predictive model but to follow a **complete and structured machine learning workflow** that reflects best practices used in real-world data science projects.

The project emphasizes:

* Understanding the prediction problem and business context
* Proper data splitting and avoiding data leakage
* Comparing simple and advanced models
* Evaluating both model performance (discrimination) and probability quality (calibration)
* Making informed decisions when selecting the final model

Rather than focusing solely on achieving high accuracy, this assignment prioritizes **process, reasoning, and correct evaluation techniques**.


 🔷 2. Business Context

The model is designed to support financial institutions and risk management teams in identifying companies that are at risk of bankruptcy.

Key Business Consideration:

* **False negatives (predicting a company as safe when it is actually bankrupt)** are more costly than false positives.

This means:

* Missing a risky company can lead to financial losses
* It is acceptable to flag some healthy companies as risky if it helps detect more bankrupt ones

As a result, the model is designed to prioritize **recall and risk detection**, which directly influences:

* Metric selection
* Threshold tuning
* Model evaluation strategy

 🔷 3. Dataset Description

The dataset used for this project is provided as part of the workshop materials.

* **File Used:** `training/data.csv`
* **Number of Rows:** ~6,819
* **Number of Features:** 96
* **Target Variable:** `Bankrupt?`

Class Distribution:

* Bankrupt (1): ~3.2%
* Not Bankrupt (0): ~96.8%

This indicates a **highly imbalanced dataset**, where the minority class (bankrupt companies) is significantly underrepresented.

Implication:

A model that predicts all companies as non-bankrupt would still achieve high accuracy, making accuracy a misleading metric. Therefore, more appropriate evaluation metrics are required.


🔷 4. Machine Learning Workflow

The project follows a structured workflow to ensure reproducibility and proper evaluation:

1. **Problem Definition**

   * Clearly defined target variable and business objective

2. **Exploratory Data Analysis (EDA)**

   * Examined dataset structure, class distribution, and missing values

3. **Data Splitting**

   * Stratified split into Train (70%), Validation (15%), and Test (15%)
   * Ensured class distribution consistency across splits

4. **Preprocessing**

   * Removed target variable from feature set
   * Handled missing values using simple imputation
   * Minimal transformation as data is already numeric

5. **Feature Engineering and Selection**

   * Created multiple feature sets to evaluate performance vs simplicity

6. **Model Training and Experimentation**

   * Tested baseline and advanced models
   * Applied imbalance handling and tuning

7. **Model Evaluation**

   * Compared models using consistent metrics

8. **Model Selection**

   * Selected best model based on validation performance

9. **Final Test Evaluation**

   * Performed final evaluation on unseen data


 🔷 5. Feature Engineering

Two feature sets were created to evaluate model performance and interpretability:

Feature Set A:

* Includes all available features after preprocessing
* Used as the primary dataset for most experiments

Feature Set B:

* Contains top 25 features selected using XGBoost feature importance
* Reduces dimensionality and improves interpretability

Purpose:

* To test whether a smaller feature set can achieve similar performance
* To understand trade-offs between model complexity and explainability

 🔷 6. Models and Experiments

Five experiments were conducted using a consistent evaluation framework:

1. **Logistic Regression (Baseline Model)**

   * Provides a simple benchmark for comparison

2. **XGBoost (Baseline)**

   * First advanced model using all features

3. **XGBoost with Class Imbalance Handling**

   * Adjusts for class imbalance using `scale_pos_weight`

4. **XGBoost with Hyperparameter Tuning**

   * Improves performance by adjusting parameters such as:

     * max_depth
     * learning_rate
     * n_estimators
     * subsample

5. **XGBoost with Selected Features (Feature Set B)**

   * Evaluates performance using fewer features

 🔷 7. Evaluation Metrics

Due to class imbalance, accuracy is not suitable as a primary metric.

 Primary Metric: PR-AUC (Precision-Recall AUC)

* Focuses on performance of the minority class
* Measures how well the model ranks bankrupt companies above non-bankrupt ones
* More informative than ROC-AUC in imbalanced datasets

 Calibration Metric: Brier Score

* Measures the accuracy of predicted probabilities
* Lower values indicate better probability calibration

 Secondary Metrics:

* ROC-AUC
* Precision
* Recall
* F1-score

These metrics provide additional insight into model performance at a chosen threshold.

 🔷 8. Model Selection Strategy

The final model was selected based on validation performance using the following criteria:

1. Highest PR-AUC (primary metric)
2. Lower Brier score (better probability quality)
3. Acceptable overfitting gap (difference between train and validation performance)
4. Simpler model when performance differences are small

The test set was strictly reserved for final evaluation and was not used during model selection.

🔷 9. Final Model

* **Model:** XGBoost (Tuned)
* **Feature Set:** A
* **Threshold:** 0.3

 Threshold Justification:

A lower threshold increases recall, allowing the model to identify more bankrupt companies. This aligns with the business goal of minimizing missed risk cases.

 🔷 10. Results

The final model demonstrates strong performance in identifying high-risk companies.

Key outcomes:

* Improved detection of bankrupt companies compared to baseline
* Balanced trade-off between precision and recall
* Reasonable probability calibration

Detailed results, including:

* Experiment comparison table
* Evaluation metrics
* Confusion matrix
* Calibration analysis

are available in the notebook and summary report.

🔷 11. Model Interpretation

Feature importance from XGBoost was used to understand key drivers of predictions.

 Observations:

* Top features are consistent with financial risk indicators
* Model provides meaningful insights for decision-making

 Limitation:

* Feature importance does not imply causation
* Does not fully capture complex feature interactions.

 🔷 12. Project Structure

assignment5/
│
├── arthi_reesu_assignment5.ipynb
├── summary_report.pdf
├── README.md

🔷 13. AI Usage

AI tools (Codex in VS Code) were used to assist in the development process:

* Generating reusable evaluation functions
* Debugging errors and improving code structure
* Assisting with metric calculations and visualizations

 Validation:

All outputs were reviewed and verified manually.

 Correction:

Initial suggestions prioritizing accuracy were corrected to use PR-AUC due to class imbalance.

 Conclusion

This project demonstrates a complete and structured approach to solving an imbalanced classification problem.

The tuned XGBoost model achieved strong performance in detecting bankrupt companies while maintaining reasonable probability calibration. The use of appropriate metrics such as PR-AUC and Brier score ensured that both classification quality and probability reliability were properly evaluated.

Overall, the model provides a practical and interpretable solution for supporting financial risk assessment and decision-making.
