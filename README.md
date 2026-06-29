<h1 align="center">🚢 Titanic Survival Prediction</h1>
<p align="center"><b>A Kaggle competition solution predicting Titanic passenger survival using Logistic Regression and Random Forest with title-based age imputation</b></p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat&logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Kaggle-Competition-20BEFF?style=flat&logo=kaggle&logoColor=white" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat" />
</p>

🇹🇷 [Türkçe](README.tr.md) | 🇬🇧 English

---

## 📌 Overview

**Titanic Survival Prediction** is a binary classification project built for the [Kaggle Titanic competition](https://www.kaggle.com/competitions/titanic). The goal is to predict which passengers survived the disaster based on features such as age, sex, ticket class, and fare. The project includes thorough exploratory data analysis, careful missing value handling (including title-based age imputation), feature engineering, and model evaluation via 5-fold cross-validation.

---

## ✨ Features

- 📊 **Comprehensive EDA** — survival rate analysis by class, sex, age, fare, and embarkation port using Plotly, Seaborn, and Missingno
- 🧹 **Smart missing value imputation** — age filled by title-group median (Mr, Mrs, Miss, Master, Rare), fare by Pclass median, Embarked by mode
- 🏷️ **Title feature engineering** — passenger titles extracted from names and grouped into meaningful categories
- 🤖 **Two models compared** — Logistic Regression (with StandardScaler) vs. Random Forest, both evaluated with 5-fold CV
- 📤 **Kaggle submission ready** — `submission.csv` generated in the required format

---

## 📁 Project Structure

```
titanic-survival-prediction/
├── titanic-disaster.ipynb   # Full notebook (EDA, preprocessing, modeling, submission)
├── README.md                # English documentation
└── README.tr.md             # Turkish documentation
```

> The `train.csv` and `test.csv` dataset files are not included in this repository. Download them from the [Kaggle Titanic competition page](https://www.kaggle.com/competitions/titanic/data).

---

## 📊 Dataset

The [Kaggle Titanic dataset](https://www.kaggle.com/competitions/titanic/data) contains passenger information from the RMS Titanic disaster (1912).

| Property | Value |
|---|---|
| **Train samples** | 891 |
| **Test samples** | 418 |
| **Target variable** | `Survived` (0 = No, 1 = Yes) |
| **Class balance** | ~61.6% did not survive, ~38.4% survived |

**Features used after preprocessing:**

| Feature | Description |
|---|---|
| `Pclass` | Ticket class (1 = 1st, 2 = 2nd, 3 = 3rd) |
| `Sex` | Gender (label encoded) |
| `Age` | Age in years (imputed via title-group median) |
| `SibSp` | Number of siblings/spouses aboard |
| `Parch` | Number of parents/children aboard |
| `Fare` | Passenger fare (imputed via Pclass median) |
| `Embarked_Q`, `Embarked_S` | Embarkation port (one-hot encoded) |
| `Title_Miss`, `Title_Mr`, `Title_Mrs`, `Title_Rare` | Title extracted from name (one-hot encoded) |

> Dropped: `Name`, `Ticket`, `Cabin` (77% missing), `PassengerId`

---

## ⚙️ Preprocessing Pipeline

1. **Embarked** — 2 missing values filled with the mode (`S` / Southampton)
2. **Fare** — 1 missing value in test set filled with the Pclass-group median from the training set
3. **Age** — 177 train / 86 test missing values filled using the median age per title group (e.g. `Master` → 3.5, `Mr` → 30.0, `Miss` → 21.0, `Mrs` → 35.0, `Rare` → 48.5)
4. **Cabin** — dropped due to ~77% missingness
5. **Title** — extracted from `Name` via regex; rare titles (`Lady`, `Countess`, `Dr`, `Rev`, etc.) grouped into `Rare`; aliases normalized (`Mlle` → `Miss`, `Ms` → `Miss`, `Mme` → `Mrs`)
6. **Encoding** — `Sex` label encoded; `Embarked` and `Title` one-hot encoded (`drop_first=True`)
7. **Scaling** — `StandardScaler` applied to numeric features for Logistic Regression only; Random Forest uses unscaled data

---

## 🤖 Models

Both models were evaluated using **5-fold cross-validation accuracy** on the training set.

| Model | CV Accuracy |
|---|---|
| **Logistic Regression** | 82.38% |
| **Random Forest** | 82.38% |

Random Forest was selected for the final Kaggle submission.

---

## 📈 Key EDA Findings

- **Sex** — women had a survival rate nearly 3× higher than men ("women and children first" evacuation protocol)
- **Pclass** — 1st class passengers had significantly higher survival rates; 3rd class showed the highest death toll
- **Fare** — positive correlation with survival (+0.26); higher fares associated with higher survival
- **Age** — children (0–10) showed higher survival rates than adults; weak negative correlation overall (−0.077)

---

## 🚀 Getting Started

```bash
git clone https://github.com/KubraParmak/titanic-survival-prediction.git
cd titanic-survival-prediction
pip install -r requirements.txt
```

Then download `train.csv` and `test.csv` from [Kaggle](https://www.kaggle.com/competitions/titanic/data), place them in the project folder, and run the notebook.

<details>
<summary>📦 Required dependencies</summary>

```
pandas
numpy
scikit-learn
matplotlib
seaborn
plotly
missingno
```
</details>

---

## 🛠️ Tech Stack

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white" />
  <img src="https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white" />
  <img src="https://img.shields.io/badge/Plotly-3F4F75?style=flat&logo=plotly&logoColor=white" />
  <img src="https://img.shields.io/badge/Seaborn-gray?style=flat" />
  <img src="https://img.shields.io/badge/Kaggle-20BEFF?style=flat&logo=kaggle&logoColor=white" />
</p>

---

## 📄 License

This project is licensed under the **MIT License**.

---

## 🙋 Author

**Kübra Parmak**
- GitHub: [@KbrPrmk](https://github.com/KbrPrmk)
- Hugging Face: [@KubraParmak](https://huggingface.co/KubraParmak)
