# 🚢 Titanic Survival Prediction (Machine Learning Project)

![Python](https://img.shields.io/badge/Python-3.10-blue)
![ML](https://img.shields.io/badge/MachineLearning-Project-green

## 📌 Project Overview

This project aims to predict passenger survival on the Titanic dataset using a machine learning approach. The workflow includes data preprocessing, feature engineering, model training, and evaluation using cross-validation.

---

## 🎯 Objective

To build a classification model that predicts whether a passenger survived:

> **0 = Did not survive, 1 = Survived**

---

## 📂 Dataset

- Source: Kaggle Titanic Competition
- Files used:
  - `train.csv`
  - `test.csv`

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

---

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

---

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

Random Forest Classifier

Model parameters:
```bash
n_estimators = 250
max_depth = 6
min_samples_leaf = 3
random_state = 42
```

---

## 📈 Model Evaluation

* Method: 5-Fold Cross Validation

Output example:

```
Cross-Validation Scores: [...]
Average Accuracy: XX%
```

👉 Model performance is evaluated using cross-validation instead of train-test split.

---

## 📤 Prediction & Output

Predictions generated on test dataset
* Output file:
* submission.csv

Format:
| PassengerId | Survived |
| ----------- | -------- |

---

## 🚀 How to Run

```bash
git clone https://github.com/yourusername/titanic-ml-project.git
cd titanic-ml-project
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

✨ Author

Developed by Kübra Parmak

---

