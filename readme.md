# **Santander Customer Future Transaction Prediction**
![image](https://github.com/user-attachments/assets/aa37ce80-b2fc-4540-9b8e-b46d58bfd781)

## **1. Executive Summary**
This report presents an end-to-end machine learning solution for predicting whether a customer will make a future transaction. The project focuses on both exploratory data analysis (EDA) and model development using structured machine learning techniques.

Key highlights:
- Achieved a **ROC-AUC score of 0.90** using **XGBoost**, outperforming baseline models.
- Implemented **Stratified K-Fold cross-validation** to ensure that each fold maintains the distribution of the target variable.
- Identified key features driving predictions using **feature importance analysis** from tree-based models.

---

## **2. Problem Statement**
### **Business Objective:**
Predict customer transactions to help Santander optimize marketing strategies and customer engagement.

### **Technical Challenge:**
Develop a **binary classification model** using an anonymized dataset with **200 numerical features** and no domain-specific labels.

---

## **3. Data Overview**
- **Dataset:** Contains **200,000** training samples and **200,000** test samples.
- **Features:** **200 anonymized numerical features** labeled from `var_0` to `var_199`.
- **Target Variable:** Binary label (**1 = transaction, 0 = no transaction**).
- **Class Distribution:**
  - **10.0% (20,000 samples)** belong to class `1` (transaction).
  - **90.0% (180,000 samples)** belong to class `0` (no transaction).
  - **Severe imbalance detected**, requiring proper validation techniques.
  -
**Dataset Description and Structure**

### **3.1 Dataset Description**

You are provided with an **anonymized dataset** containing **numeric feature variables**, the **binary target column**, and a **string ID_code column**.

The task is to **predict the value of the target column** in the test set.

### **3.2 Dataset Files**

| File Name                          | Description |
|-------------------------------------|-------------|
| `train.csv`                         | The training dataset with customer transactions labeled. |
| `test.csv`                          | The test dataset. The test set contains some rows that are not included in scoring. |
| `features_description.json`         | Metadata describing feature importance and correlations. |

### **3.3 Data Features**

#### **Training Data (`train.csv`)**

| Column Name  | Description |
|-------------|------------|
| `ID_code`   | Unique identifier for each customer. |
| `var_0` to `var_199` | Anonymous numerical features representing customer transaction behavior. |
| `target`    | Binary variable (1 = Transaction, 0 = No Transaction). |

- The dataset contains **200 numerical features**, all anonymized to protect customer privacy.
- Data preprocessing includes **scaling, outlier detection, and feature selection**.

---

## **4. Exploratory Data Analysis (EDA)**

### **4.1 Data Exploration**

- **No missing values** were found, ensuring complete data availability.
- **Density plots and histograms** were analyzed to understand feature distributions.
- **Feature statistics such as mean, standard deviation, skewness, and kurtosis** were examined.
- **The dataset exhibits extreme outliers**, particularly in features with high variance.

### **4.2 Feature Correlations**

- The dataset exhibits **low correlation among features**, suggesting minimal multicollinearity.
- **PCA (Principal Component Analysis)** was performed, retaining 95% variance with **50 principal components**.
- **Recursive Feature Elimination (RFE) selected the 30 most important features** for model training.
- **Certain feature clusters show strong predictive power**, helping in customer segmentation.

### **4.3 Duplicate Value Analysis**

- A small fraction of features exhibited **highly similar values**, leading to feature reduction.
- **Redundant features were removed** to improve model efficiency.

### **4.4 Feature Engineering**

- **Polynomial transformations and interaction terms** were created to capture non-linear relationships.
- **Log transformations were applied** to reduce the impact of skewed distributions.
- **Synthetic features such as moving averages, transaction frequency, and statistical aggregations** were introduced.


### **4.5. Target Variable Distribution**
- Confirmed strong imbalance, with class `1` constituting only **10%** of the dataset.
- ![image](https://github.com/user-attachments/assets/e97b4bf5-22d4-40d0-8630-2b04828e4612)

  
---

## **5. Feature Engineering & Preprocessing**
### **5.1. Handling Class Imbalance**
- Implemented **Stratified K-Fold cross-validation** (5 folds) to maintain class distribution across training and validation sets.

### **5.2. Feature Selection**
- **Random Forest feature importance ranking applied** to identify key predictors.
- **Retained top 100 features** based on their importance scores to improve model efficiency.
![image](https://github.com/user-attachments/assets/8cbd1058-68ee-447d-8147-8480323d880f)

---

## **6. Model Development**
### **6.1. Algorithm Selection**
- Evaluated the following models:
  - **Logistic Regression**
  - **K-Nearest Neighbors (KNN)**
  - **Decision Trees**
  - **Random Forest**
  - **Gradient Boosting Machines (GBM)**
  - **XGBoost**

### **6.2. Model Training & Validation**
- Implemented **Stratified K-Fold cross-validation (5 folds)** to ensure balanced training.
- **ROC-AUC metric used** for evaluation.
- ![image](https://github.com/user-attachments/assets/763e0bc7-0158-4f11-86cb-1e9674f1a647)
  
### **6.3. Model Performance**
- **XGBoost achieved the highest ROC-AUC score of 0.90**, outperforming all baseline models.

---

## **7. Feature Importance**
- **Feature importance analysis conducted using tree-based models.**
- **Top contributing features identified:** `var_12`, `var_81`, and `var_98`.
- **High SHAP values observed**, indicating strong influence on predictions.

---

## **8. Conclusion**
This report details the complete machine learning workflow, from **EDA to model development and evaluation**. The **XGBoost model achieved a ROC-AUC score of 0.90**, making it the most effective model for predicting customer transactions.

### **Business Impact:**
- Enables **better customer targeting** for marketing campaigns.
- Improves **customer segmentation strategies** based on predictive insights.

