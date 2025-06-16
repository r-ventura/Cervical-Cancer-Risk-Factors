
# Cervical Cancer Risk Factors Analysis

This project explores the relationship between cervical cancer and demographic, behavioral, and clinical factors using machine learning models to predict the likelihood of a positive diagnostic test. Developed for the *Aprenentatge Automàtic I* (Machine Learning I) course at **Universitat Politècnica de Catalunya (UPC)**.

## 📌 Project Context

Cervical cancer is a significant global health issue. This study aims to provide valuable insights for early detection, prevention, and intervention by exploring various external factors influencing its appearance.

## 🏆 Main Objectives

* Identify the most important external factors associated with cervical cancer.
* Create accurate models to classify samples as positive or negative for cervical cancer.
* Compare different models to determine the best performer in predicting cervical cancer.

## 📊 Dataset Information

The study uses a multivariate dataset covering demographic information, habits, and historical medical records of 858 patients. It was collected at the Hospital Universitario de Caracas in Venezuela. The dataset contains 36 attributes, including numerical and categorical variables, with missing values present.
The original target variables (Hinselmann, Schiller, Cytology, and Biopsy) are diagnostic procedures for cervical cancer detection. For this study, a new binary target variable named `Cancer` was created to indicate a positive diagnosis based on any of these tests.

## ⚙️ Methodology

### 1. Data Exploration and Pre-processing

The initial dataset inspection revealed numerical and binary categorical variables, some with inadequate float formats. A comprehensive pre-processing pipeline was implemented to address data quality issues:
* **Missing Values:** Removed `STDs: Time since first diagnosis` and `STDs: Time since last diagnosis` due to extensive missing values. Remaining instances with missing values were then removed, resulting in 668 instances and 34 features.
* **Outliers:** Identified and removed outliers in `Age`, `Number of sexual partners`, and `Smokes (packs/year)` based on histogram and box-plot analysis. Variables with mostly zero values were also removed if `Smokes`, `Hormonal Contraceptives`, `IUD`, and `STDs` already captured the information.
* **Mixed Data Types:** Categorical variables were encoded into integers (0s and 1s) for appropriate formatting. Columns `STDs: cervical condylomatosis` and `STDs: AIDS` were removed as they only contained a single value. This left 662 instances and 22 variables.
* **Normalization:** Data was normalized using a small non-zero value added to variables with zeros (e.g., `Num of pregnancies`) to enable Box-Cox transformation, followed by Min-Max scaling to a [0,1] range.
* **Addressing Data Imbalance:** Identified and removed 6 STDs variables that did not contribute sufficient information due to data imbalance, leaving 16 attributes.

### 2. Model Proposals

Various classification models were explored, including Linear Classification methods, Decision Trees, and Random Forests.
* **Linear Classification Models:** LDA (Linear Discriminant Analysis), QDA (Quadratic Discriminant Analysis), k-NN (k-Nearest Neighbors), Gaussian Naive Bayes (and variations), and Logistic Regression.
* **Decision Trees and Random Forests:** Standard and various configurations.
* **Feature Selection:** Lasso Regression, Decision Trees, and Random Forests were used to create three different dataframes (DF1: post-preprocessing, DF2: after Lasso, DF3: after DT/RF on DF2) for comparative analysis.

### 3. Resampling Protocol

Data was split into train, validation, and test sets (60% train, 20% validation, 20% test) with stratification to maintain class proportions. To address high data imbalance (less than 15% positive cases), `RandomUnderSampler` from the `imbalanced-learn` package was used to reduce the majority class by 70%.

## 📈 Key Findings

* Initial models on DF1 showed concerning performance, particularly low recall for class 1 (e.g., KNN-5 had 0.706 recall, meaning ~30% of cancer cases were misclassified), indicating challenges with data imbalance and model effectiveness.
* Feature selection methods were applied to try and improve these results, with further analysis conducted on DF2 and DF3.
* The study emphasizes the critical importance of maximizing recall and F1 score for class 1 to minimize false negatives in health risk factor prediction.
* Age, Number of sexual partners, First sexual intercourse, Smokes, Hormonal Contraceptives, IUD, and STDs:condylomatosis have seemed to be the most relevant factors, though expert consultation is recommended for definitive conclusions.

## 🛠️ Tools & Libraries

* `imbalanced-learn` (for `RandomUnderSampler`)
* Python libraries for data manipulation, visualization, and machine learning models (e.g., `sklearn`).
