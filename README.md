
# Titanic Survival Prediction

This project predicts Titanic passenger survival using **machine learning models**. It covers data preprocessing, feature engineering, model training, evaluation, and hyperparameter tuning.

---

## **Project Overview**

The goal of this project is to:
- Analyze the Titanic dataset
- Build predictive models to classify passengers as **Survived (1)** or **Not Survived (0)**
- Evaluate the performance of models using multiple metrics
- Tune model parameters for optimal performance

---

## **Workflow**

### 1. **Data Loading**
- Load `train.csv` for model training.
- Load `test.csv` for evaluation.
- Load `gender_submission.csv` (used as ground truth labels for test data).

---

### 2. **Exploratory Data Analysis**
- Print dataset information (`.info()`, `.describe()`).
- Visualize:
  - Gender distribution
  - Age group distribution (Child, Teen, Adult, Elder)
  - Passenger class distribution (1st, 2nd, 3rd)

---

### 3. **Data Preprocessing**

#### **Irrelevant Columns**
- Remove `PassengerId` and `Ticket`.

#### **Handle Missing Values**
- **Age:** Fill missing values with the median.
- **Fare (test data):** Fill with median.
- **Embarked:** Fill with most frequent port.
- **Cabin:** Convert to a binary feature (`1` if present, `0` if missing).

---

### 4. **Encoding Categorical Features**
- **Sex:** Encode as `0` for male and `1` for female.
- **Embarked:** Apply one-hot encoding.

---

### 5. **Feature Engineering**

#### **Title Extraction**
- Extract passenger titles (Mr, Mrs, Miss, etc.) from names.
- Group rare titles into a single category ("Rare") and encode:
  - Rare = 1
  - Common = 0

#### **Age Binning**
- Group ages into: Child (0–10), Teen (11–18), Adult (19–49), Elder (50+).
- Convert these groups into a binary feature:
  - Teen/Adult = 1
  - Child/Elder = 0

---

### 6. **Modeling**

#### **Models Used**
- **Logistic Regression**
- **Random Forest Classifier**

#### **Validation**
- Perform **5-fold cross-validation** on training data.
- Print mean accuracy for each model.

#### **Training**
- Fit models on the entire training dataset.

---

### 7. **Evaluation**

- Evaluate models on:
  - Training data
  - Test data (`test.csv` with labels from `gender_submission.csv`)
- Metrics:
  - Accuracy
  - Precision
  - Recall
  - Confusion matrix (visualized using heatmaps)

---

### 8. **Hyperparameter Tuning**

- Use **RandomizedSearchCV** to tune Logistic Regression:
  - Parameter grid:
    - `C`: 20 values between 10^-0.9 and 10^0.9 (logarithmic scale)
    - `solver`: `liblinear`
  - Perform 5 iterations with 5-fold cross-validation.
- Output:
  - Best hyperparameters
  - Best cross-validation score

---

## **Results**
- Cross-validation accuracy for both models.
- Training and test accuracy scores.
- Confusion matrices and metrics to analyze prediction performance.
- Optimized Logistic Regression model parameters.

---

## **Technologies Used**

- **Python 3**
- **Libraries:**
  - pandas
  - numpy
  - matplotlib
  - scikit-learn

---

## **How to Run**

1. Clone this repository:
   ```bash
   git clone <repo-url>
   ```
2. Place `train.csv`, `test.csv`, and `gender_submission.csv` in the project directory.
3. Run the notebook or Python script:
   ```bash
   python titanic_prediction.py
   ```
4. View printed metrics and confusion matrix plots.

---

## **Key Learnings**
- Handling missing data and feature engineering significantly impact model accuracy.
- Random Forest tends to fit the data better, but Logistic Regression generalizes well when tuned.
- Regularization (controlled by `C`) is critical for avoiding overfitting in Logistic Regression.
