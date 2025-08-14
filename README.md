# Lab 5 Report

## 1. EDA and Insights

+ Class imbalance: The dataset is highly skewed toward non-bankrupt companies, requiring specific strategies for minority class handling.

+ Feature distributions: Several financial ratios are right-skewed, suggesting the need for transformation or scaling.

+ Correlation patterns: Multiple variables exhibit strong pairwise correlations, indicating potential multicollinearity concerns.

+ Outlier detection: Certain extreme ratio values may represent rare but meaningful early warning signals of financial distress.


## 2. Selected Features and Preprocessing

+ Feature retention: Selected variables with both strong statistical correlation to the target and demonstrated predictive value in preliminary models.

+ Scaling approach: Applied StandardScaler to normalize numerical features for model compatibility.

+ Missing value handling: Median imputation used to reduce sensitivity to extreme values.

+ Encoding: One-hot encoding applied to categorical variables to enable model ingestion.

+ Data splitting: Stratified train-test split ensured proportional class representation across sets.


## 3. Hyperparameter Tuning Outcomes

+ Optimization method: Hyperopt with stratified cross-validation.

+ Key tuned parameters:

    - n_estimators: Adjusted for optimal balance between bias and variance.

    - max_depth: Controlled tree complexity to avoid overfitting.


    - learning_rate: Maintained at a conservative value to enhance stability.


    - subsample and colsample_bytree: Tuned to manage variance and improve generalization.


    - min_child_weight: Prevented overfitting on small, noisy data segments.


## 4. Model Performance Comparison

+ XGBoost:

    - Highest ROC-AUC on both train and test sets.

    - Balanced precision and high recall.

    - Strong F1-score performance.

+ Random Forest:

    - Slightly lower ROC-AUC compared to XGBoost.

    - Good precision but moderate recall.

    - Moderate F1-score.

+ Logistic Regression:

    - Lower ROC-AUC relative to tree-based models.

    - Lower precision, recall, and F1-score across the board.


## 5. Calibration curves, ROC-AUC curves, Brier Scores

+ Calibration curves: XGBoost displayed strong probability alignment with actual outcomes, with minor overconfidence at higher predicted probabilities.


+ ROC-AUC: All tested models exceeded 0.85; XGBoost led in overall discrimination.


+ Brier score: XGBoost recorded the lowest value, indicating superior probability prediction accuracy.


## 6. SHAP summary plots

+ Most influential predictors:

    - Liquidity ratios

    - Debt-to-equity ratio

    - Profitability ratios

    - Cash flow indicators


+ Impact direction:

    - Higher leverage (debt load) increases bankruptcy likelihood.

    - Lower liquidity significantly elevates default risk.


## 7. PSI results and drift analysis

+ Population Stability Index (PSI):

    - Majority of variables had PSI < 0.1, indicating stability.

    - A few features recorded PSI between 0.1 and 0.2, suggesting mild drift potentially linked to macroeconomic trends.

+ No severe drift detected, periodic monitoring recommended for early warning.


## Questions

### What were the main challenges you faced during implementation, and how did you overcome them?

    Keeping everything lightweight. I resolved it by modest spaces, matplotlib-only plots, SHAP sampled to 200 rows and PSI with 10 quantile bins.

### How did your Lab 4 research influence your Lab 5 implementation?

    It helped me understand what I had to do and which methods to use at every step, but I’ll be honest, I had to deviate a bit from my Lab 4 after attending class the day after submission. I realized that some of my decisions were not the best, like using SMOTE and PR-AUC. Also, I didn’t mention using things like ROC-AUC and Briar Score.

### Based on your evaluation, which model would you recommend for deployment, and why?

    XGBoost was the best model because it has the highest recall and still had a balanced F1, meaning good precision despite the high recall. XGBoost also had a strong ROC-AUC performance across both train and test sets (above 0.85). XGBoost also had the lowest Briar score, indicating superior probability prediction accuracy.
