# Android App Malware Detection via Permissions

This repository contains a machine learning pipeline designed to classify Android applications as either Benign or Malware based on their requested device permissions[cite: 1]. 

## Dataset Overview
* **Size:** 2,300 Android applications[cite: 1].
* **Features:** 113 columns primarily consisting of binary permission flags (e.g., `READ_EXTERNAL_STORAGE`, `ACCESS_DOWNLOAD_MANAGER`, `SET_ALARM`)[cite: 1].
* **Target Variable:** The `Class` column, where `1` indicates Malware and `0` indicates a Benign app[cite: 1].

## Project Process
1. **Data Preprocessing:** Handled missing data by filling null values with column means[cite: 1]. The Android App names were moved to the DataFrame index to exclude them from model training[cite: 1].
2. **Exploratory Data Analysis:** Evaluated class distributions visually using pie charts to understand the dataset's baseline balance[cite: 1].
3. **Data Splitting:** Divided the dataset into a 60% training set and a 40% testing set[cite: 1].
4. **Baseline Modeling:** Trained and evaluated multiple classifiers on the raw data, including Logistic Regression, Gaussian Naive Bayes, Decision Tree, Support Vector Machine (SVM), Random Forest, and XGBoost[cite: 1].
5. **Addressing Class Imbalance:** Applied `RandomOverSampler` and `RandomUnderSampler` (with a 0.9 sampling strategy) to rebalance the training data[cite: 1]. Core models were retrained on these sampled datasets to compare performance shifts[cite: 1].
6. **Dimensionality Reduction:** Implemented Principal Component Analysis (PCA) to compress the feature space into 10 principal components, plotted the variance, and evaluated the inverse transformation[cite: 1].

## Inferences & Model Performance
* **Baseline Models:** On the unsampled dataset, XGBoost yielded the highest training accuracy (0.78) and a test accuracy of 0.66[cite: 1]. Tree-based models (Random Forest, Decision Tree), SVM, and Logistic Regression achieved extremely high recall scores (0.95–0.99) but had ROC AUC scores hovering around 0.50 to 0.51, indicating a bias toward predicting the majority class[cite: 1].
* **Naive Bayes Anomaly:** Gaussian Naive Bayes achieved a high training accuracy (0.91) and the best baseline test accuracy (0.70), but it suffered from an exceptionally low recall score (0.06)[cite: 1].
* **Sampling Impact:** Rebalancing the dataset altered the performance dynamics[cite: 1]. For example, the Decision Tree model trained on oversampled data achieved an improved ROC AUC of 0.59 and a recall of 0.54, compared to the baseline[cite: 1]. Undersampling yielded a recall of 0.80 and an ROC of 0.53[cite: 1]. This highlights the inherent trade-off between capturing true malware (recall) and avoiding false positives.

## Dependencies
The notebook requires the following Python libraries[cite: 1]:
* `numpy` & `pandas`
* `matplotlib` & `seaborn`
* `scikit-learn`
* `imbalanced-learn`
* `xgboost`
* `pydotplus`
