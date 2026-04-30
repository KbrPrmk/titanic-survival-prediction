# 🚢 Titanic Survival Prediction (Machine Learning Project)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Project-green)
![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![Scikit-learn](https://img.shields.io/badge/Scikit--Learn-ML-orange?logo=scikit-learn)
![Model](https://img.shields.io/badge/Model-Random%20Forest-darkgreen)

## 📌 Project Overview

This project aims to predict passenger survival on the Titanic dataset using a machine learning approach. The workflow includes data preprocessing, feature engineering, model training, and evaluation using cross-validation.

---

## 🎯 Objective

To build a classification model that predicts whether a passenger survived:

> **0 = Did not survive, 1 = Survived**

---

## 📂 Dataset

This project uses the Titanic dataset from the Kaggle Titanic Competition.

**Source:** https://www.kaggle.com/competitions/titanic

### 📊 Dataset Description

The dataset contains information about passengers aboard the Titanic, including demographic details and travel information. It is used to predict whether a passenger survived the disaster.

### 📁 Files Used

- `train.csv` → Contains features and target variable (Survived)
- `test.csv` → Contains features only (used for prediction)

---

### 🧾 Key Features

| Feature   | Description |
|----------|------------|
| Pclass   | Passenger class (1 = Upper, 3 = Lower) |
| Sex      | Gender of passenger |
| Age      | Age in years |
| SibSp    | Number of siblings/spouses aboard |
| Parch    | Number of parents/children aboard |
| Fare     | Ticket fare |
| Embarked | Port of embarkation |

---

### 🎯 Target Variable

| Variable | Meaning |
|---------|--------|
| Survived | 0 = Did not survive, 1 = Survived |

---

### ⚠️ Data Challenges

- Missing values in:
  - Age
  - Fare
  - Embarked  

- Categorical variables required encoding:
  - Sex
  - Embarked  

---

## ⚙️ Technologies Used

- Python 🐍
- Pandas
- NumPy
- Seaborn & Matplotlib 📊
- Scikit-learn

---

## 🔍 Data Preprocessing

### Missing Value Handling

- `Age` → filled with median
- `Fare` → filled with median (test set)
- `Embarked` → filled with mode


### Encoding

- `Sex`:
  - female → 1
  - male → 0

- `Embarked`:
  - One-hot encoding applied
  - Features:
    - Embarked_C
    - Embarked_Q
    - Embarked_S


### Feature Selection

Initial features:

```text
Pclass, Sex, Age, SibSp, Parch, Fare, Embarked_C, Embarked_Q, Embarked_S
```

Final model features:

```text
Pclass, Sex, Fare, Embarked_C, Embarked_Q, Embarked_S
```

---

## 📊 Exploratory Data Analysis

* Correlation heatmap created using seaborn
* Relationships between numerical features analyzed

---

## ⚖️ Feature Scaling
StandardScaler applied to:
* Age
* Fare

---

## 🤖 Model

### Random Forest Classifier

Model parameters:
```bash
n_estimators = 250
max_depth = 6
min_samples_leaf = 3
random_state = 42
```

---

## 🤖 Why Random Forest?

Random Forest was chosen because:

- Handles both numerical and categorical features well  
- Reduces overfitting through ensemble learning  
- Performs well on structured/tabular datasets like Titanic  
- Robust to noise and missing values
  
---

## 📈 Model Evaluation

* Method: 5-Fold Cross Validation

Output example:

```
Cross-Validation Scores: [0.7877095  0.78651685 0.84831461 0.80337079 0.80337079]
Average Accuracy: 80.59%
```

---

## 📤 Prediction & Output

Predictions are generated on the test dataset.

- Output file: `submission.csv`

Format:
| PassengerId | Survived |
| ----------- | -------- |

---

## 🚀 How to Run

```bash
git clone https://github.com/KbrPrmk/titanic-survival-prediction.git
cd titanic-survival-prediction
```

```bash
pip install -r requirements.txt
```

```bash
jupyter notebook
```

Open:

```bash
titanic-disaster.ipynb
```

---

## 🧠 Key Points
* Missing values handled using statistical methods (median, mode)
* Categorical variables encoded properly
* Feature scaling applied to numerical variables
* Random Forest used as main model
* Cross-validation ensures robust evaluation

--- 

## 🔮 Possible Improvements
* Hyperparameter tuning (GridSearchCV)
* Adding new features (e.g. Family Size)
* Trying different models (XGBoost, SVM)

---

## ⭐ Project Status

✔ Completed  

---

Developed by **Kübra Parmak**
