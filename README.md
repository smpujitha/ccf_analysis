<img width="403" height="135" alt="image" src="https://github.com/user-attachments/assets/80ad7b88-427b-4ed4-9dac-40b6e8091d6c" /># ccf_analysis
# Credit Card Fraud Detection Using Machine Learning

## 1. Project Overview

Credit card fraud detection is a machine learning classification problem in which the objective is to identify whether a transaction is legitimate or fraudulent.

In this project, machine learning models are trained to classify transactions into two classes:

- 0 → Legitimate transaction
- 1 → Fraudulent transaction

The main challenge of this project is the highly imbalanced nature of the dataset, where fraudulent transactions represent only a very small portion of all transactions.

The project focuses on data exploration, preprocessing, handling class imbalance, model training, model evaluation, model comparison, and final model selection.

---

## 2. Problem Statement

The objective of this project is to develop a machine learning system that can detect fraudulent credit card transactions.

The system should:

- Explore and understand the transaction dataset.
- Identify patterns associated with fraudulent transactions.
- Handle the highly imbalanced target variable.
- Train multiple machine learning classification models.
- Evaluate the models using suitable classification metrics.
- Select the most suitable model for fraud detection.
- Provide insights that can help reduce financial losses caused by fraudulent transactions.

---

## 3. Dataset

The dataset contains credit card transaction information.

The dataset includes approximately 284,807 transactions, with only 492 fraudulent transactions.

The target variable is:

`Class`

where:

- `0` represents a legitimate transaction.
- `1` represents a fraudulent transaction.

The dataset contains the following major types of variables:

- `Time`
- `Amount`
- `V1` to `V28`
- `Class`

The features `V1` to `V28` are PCA-transformed features.

---

## 4. Why PCA-Transformed Features Are Used

The original transaction information contains sensitive financial information.

To protect privacy, many of the original variables have been transformed using Principal Component Analysis (PCA).

PCA transforms the original variables into a new set of components while preserving important patterns and variation in the data.

Therefore, the features `V1` to `V28` represent transformed components rather than directly interpretable original transaction attributes.

The target variable `Class` is not PCA-transformed because it represents the actual outcome that the model needs to predict.

---

## 5. Project Objectives

The main objectives are:

1. Understand the credit card transaction dataset.
2. Perform exploratory data analysis.
3. Check missing values and duplicate records.
4. Analyze the distribution of legitimate and fraudulent transactions.
5. Identify important patterns in transaction amounts.
6. Apply appropriate preprocessing techniques.
7. Handle class imbalance using SMOTE.
8. Split the dataset into training and testing sets.
9. Train multiple machine learning models.
10. Evaluate model performance using appropriate metrics.
11. Compare the models.
12. Select a suitable final model.
13. Analyze important features.
14. Test the model on unseen data.
15. Derive business insights and recommendations.

---

# 6. Data Exploration

Exploratory Data Analysis (EDA) was performed to understand the structure and characteristics of the dataset.

The following areas were investigated:

- Dataset shape
- Data types
- Missing values
- Duplicate records
- Statistical information
- Class distribution
- Correlation between variables
- Distribution of transaction amounts
- Distribution of transaction amounts after logarithmic transformation

The class distribution showed a severe imbalance between legitimate and fraudulent transactions.

This imbalance is one of the major challenges of credit card fraud detection.

---

# 7. Data Preprocessing

## Missing Values

The dataset was checked for missing values to ensure that missing observations would not negatively affect the machine learning models.

## Duplicate Records

Duplicate records were investigated to determine whether repeated transactions represented exact duplicate rows.

## Data Types

The data types of the variables were checked to ensure that the features were suitable for machine learning algorithms.

## Feature Scaling

Standardization was applied to the numerical features.

The standardization formula is:

Z = (X - μ) / σ

where:

- X = original value
- μ = mean of the feature
- σ = standard deviation

Scaling is especially important for distance-based algorithms such as KNN.

---

# 8. Transaction Amount Transformation

The `Amount` feature showed a highly skewed distribution.

A logarithmic transformation was explored to reduce the effect of extreme values and make the distribution easier to analyze.

The logarithmic transformation helps compress very large values while preserving the relative ordering of observations.

---

# 9. Train-Test Split

The dataset was divided into training and testing sets.

The project used:

- 80% → Training data
- 20% → Testing data

Stratified splitting was used so that the class distribution of legitimate and fraudulent transactions was maintained between the training and testing sets.

The test data was kept separate so that the trained model could be evaluated on unseen observations.

---

# 10. Class Imbalance

The dataset contains a very small number of fraudulent transactions compared with legitimate transactions.

Approximately:

- 284,315 legitimate transactions
- 492 fraudulent transactions

This creates a severe class imbalance.

If a model simply predicted every transaction as legitimate, it could still achieve very high accuracy while completely failing to detect fraud.

Therefore, accuracy alone is not sufficient for evaluating this problem.

---

# 11. SMOTE

SMOTE stands for:

**Synthetic Minority Oversampling Technique**

SMOTE was used to address the class imbalance in the training data.

Instead of simply duplicating existing fraudulent transactions, SMOTE creates synthetic minority-class observations using existing minority observations and their nearest neighbors.

The purpose is to provide the model with more representative fraud patterns during training.

SMOTE was applied to the training data rather than the test data.

The test set remained untouched so that model performance could be evaluated on the original unseen distribution.

---

# 12. Machine Learning Models

Four machine learning classification models were trained and evaluated.

## 12.1 Logistic Regression

Logistic Regression was used as a baseline classification model.

It uses the sigmoid function to convert the model output into a probability between 0 and 1.

The sigmoid function is:

σ(x) = 1 / (1 + e^-x)

The probability is then converted into a class prediction using a classification threshold.

---

## 12.2 K-Nearest Neighbors

KNN classifies a new observation based on the classes of its nearest observations.

The model uses distance to identify neighboring observations.

Feature scaling is important for KNN because the algorithm depends on distance calculations.

---

## 12.3 Decision Tree

Decision Tree is a hierarchical classification algorithm.

It repeatedly divides the dataset using feature conditions and creates branches until reaching a final prediction at a leaf node.

The tree uses splitting criteria such as Gini impurity to determine suitable splits.

---

## 12.4 Random Forest

Random Forest is an ensemble learning algorithm consisting of multiple Decision Trees.

Each tree produces a prediction, and the forest combines the predictions to produce the final classification.

Random Forest was included because ensemble methods can provide more robust predictions than an individual Decision Tree.

---

# 13. Model Evaluation

The models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion Matrix

## Accuracy

Accuracy measures the proportion of all transactions that were correctly classified.

However, accuracy alone is not reliable for highly imbalanced fraud datasets.

---

## Precision

Precision answers:

> Of all transactions predicted as fraud, how many were actually fraud?

High precision means fewer legitimate transactions are incorrectly flagged as fraud.

---

## Recall

Recall answers:

> Of all the actual fraudulent transactions, how many were successfully detected?

Recall is particularly important in fraud detection because missing a fraudulent transaction can result in financial loss.

---

## F1-Score

F1-score provides a balance between precision and recall.

It is calculated using:

F1 = 2 × (Precision × Recall) / (Precision + Recall)

---

## ROC-AUC

ROC-AUC measures how well the model distinguishes between legitimate and fraudulent transactions across different classification thresholds.

A higher ROC-AUC indicates better discrimination between the two classes.

---

# 14. Model Comparison

The models produced the following results:

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.999491 | 0.870968 | 0.826531 | 0.848168 | 0.971327 |
| KNN | 0.997999 | 0.457447 | 0.877551 | 0.601399 | 0.948493 |
| Decision Tree | 0.997437 | 0.382353 | 0.795918 | 0.516556 | 0.896851 |
| Random Forest | 0.999491 | 0.870968 | 0.826531 | 0.848168 | 0.974538 |

---

# 15. Final Model Selection

Based on the evaluated results, Random Forest was selected as the final model.

Random Forest achieved:

- Accuracy: 99.9491%
- Precision: 87.10%
- Recall: 82.65%
- F1-score: 84.82%
- ROC-AUC: 97.45%

Random Forest achieved the highest ROC-AUC among the evaluated models while maintaining the same reported precision, recall, and F1-score as Logistic Regression.

KNN achieved a slightly higher recall, but its precision was substantially lower, meaning it generated more false fraud alerts.

Decision Tree produced lower precision, recall, F1-score, and ROC-AUC compared with the stronger models.

Therefore, Random Forest provides a strong overall balance for the fraud detection task.

---

# 16. Confusion Matrix

A confusion matrix was used to understand the types of predictions made by each model.

The four outcomes are:

- True Positive (TP): Fraud correctly detected as fraud.
- True Negative (TN): Legitimate transaction correctly classified as legitimate.
- False Positive (FP): Legitimate transaction incorrectly classified as fraud.
- False Negative (FN): Fraudulent transaction incorrectly classified as legitimate.

For fraud detection, both False Positives and False Negatives are important.

False Negatives can represent financial losses because fraudulent transactions are missed.

False Positives can inconvenience customers because legitimate transactions may be incorrectly blocked or flagged.

---

# 17. Feature Importance

Feature importance can be analyzed using the Random Forest model to identify which transformed features contribute most strongly to the model's decisions.

Because the dataset uses PCA-transformed features, the importance of `V1`–`V28` cannot be directly interpreted as an original business attribute such as customer age, location, or card type.

Instead, the important features represent transformed patterns in the transaction data.

---

# 18. Business Insights

The analysis provides several important business insights.

### 1. Fraud is highly rare

Only a very small percentage of transactions are fraudulent.

Therefore, businesses cannot rely on accuracy alone when evaluating fraud detection systems.

### 2. Fraud detection requires minority-class learning

Because fraudulent transactions are rare, techniques such as SMOTE can help the model learn patterns associated with the minority class.

### 3. Recall is important

A fraudulent transaction that is classified as legitimate can result in financial loss.

Therefore, fraud detection systems should carefully monitor recall.

### 4. Precision is also important

If precision is too low, many legitimate customers may receive unnecessary fraud alerts.

This can create poor customer experiences and unnecessary manual investigation.

### 5. Model selection requires a trade-off

There is a trade-off between detecting as many fraudulent transactions as possible and avoiding false alarms.

Therefore, businesses should select the model according to the cost of False Positives and False Negatives.

---

# 19. Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Imbalanced-learn
- Matplotlib
- Seaborn
- Jupyter Notebook / Google Colab

---

# 20. Project Workflow

The overall workflow followed in this project was:

Dataset
↓
Data Exploration
↓
Data Cleaning
↓
EDA
↓
Feature Scaling
↓
Train-Test Split
↓
Class Imbalance Analysis
↓
SMOTE
↓
Model Training
↓
Logistic Regression
↓
KNN
↓
Decision Tree
↓
Random Forest
↓
Model Evaluation
↓
Model Comparison
↓
Final Model Selection
↓
Feature Importance
↓
Unseen Data Prediction
↓
Business Insights
↓
Conclusion

---

# 21. Conclusion

This project demonstrates how machine learning can be applied to credit card fraud detection.

The major challenge was the severe class imbalance between legitimate and fraudulent transactions. SMOTE was used on the training data to improve the representation of fraudulent transactions during model training.

Four classification models were evaluated using accuracy, precision, recall, F1-score, ROC-AUC, and confusion matrices.

Among the evaluated models, Random Forest provided the strongest overall result based on the current evaluation, particularly its ROC-AUC of 0.974538.

The project demonstrates that fraud detection should not be evaluated using accuracy alone. Precision, recall, F1-score, ROC-AUC, and the costs associated with false positives and false negatives should also be considered.

A production fraud detection system could further improve performance through hyperparameter tuning, threshold optimization, continuous monitoring, and retraining using newly observed transaction patterns.
