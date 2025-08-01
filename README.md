
# Titanic Survival Prediction

This project predicts Titanic passenger survival using **Supervised Machine Learning Models**. It covers data preprocessing, feature engineering, model training, evaluation, and hyperparameter tuning.

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
  
 <img width="566" height="747" alt="image" src="https://github.com/user-attachments/assets/2ff9b9e2-cb12-4bb8-b826-5c689b56cb80" />
  
- Visualize:
  - Gender distribution
    
    <img width="653" height="465" alt="image" src="https://github.com/user-attachments/assets/e2c82d7e-28fa-42aa-8968-6c198d9f83ea" />

  - Age group distribution (Child, Teen, Adult, Elder)
    
    <img width="681" height="464" alt="image" src="https://github.com/user-attachments/assets/451cfd17-9e60-4aec-a8ea-62c2fd5fbb30" />

  - Passenger class distribution (1st, 2nd, 3rd)

 <img width="654" height="455" alt="image" src="https://github.com/user-attachments/assets/58469341-815f-4278-ad6d-976e26e4d78a" />

    
 

---

### 3. **Data Preprocessing**

#### **Irrelevant Columns**
- Remove `PassengerId` and `Ticket`.

  <img width="665" height="636" alt="image" src="https://github.com/user-attachments/assets/b00c4ac1-8919-46cb-972e-bfca8ef237b6" />

  <img width="623" height="598" alt="image" src="https://github.com/user-attachments/assets/588ab64a-76a4-4d93-96ea-e001a4d42b06" />



#### **Handle Missing Values**
- **Age:** Fill missing values with the median.
- **Fare (test data):** Fill with median.
- **Embarked:** Fill with most frequent port.
- **Cabin:** Convert to a binary feature (`1` if present, `0` if missing).

<img width="385" height="437" alt="image" src="https://github.com/user-attachments/assets/ed0bbadd-924b-4523-8783-5df68cbb22e5" />

<img width="350" height="405" alt="image" src="https://github.com/user-attachments/assets/26ef4fb7-d677-4f2e-84ca-22ee253e7dc5" />

---

### 4. **Encoding Categorical Features**
- **Sex:** Encode as `0` for male and `1` for female.
- **Embarked:** Apply one-hot encoding.

<img width="693" height="630" alt="image" src="https://github.com/user-attachments/assets/9a9e17f2-9d72-48f3-b80f-e05e4b38cbd2" />

<img width="640" height="611" alt="image" src="https://github.com/user-attachments/assets/1e2b037f-dcd7-42e4-8437-f726376451b1" />

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

<img width="593" height="587" alt="image" src="https://github.com/user-attachments/assets/b8a18d43-4b24-47dc-ac92-f4012bf4e8f2" />

<img width="617" height="587" alt="image" src="https://github.com/user-attachments/assets/b6628c59-2a58-46d9-8855-39031f8dc0b4" />

---

### 6. **Modeling**

#### **Models Used**
- **Logistic Regression**
- **Random Forest Classifier**

#### **Validation**
- Perform **5-fold cross-validation** on training data.
- Print mean accuracy for each model.

<img width="276" height="38" alt="image" src="https://github.com/user-attachments/assets/f6564eb9-4c99-4490-a23a-e4b0602b10fa" />


#### **Training**
- Fit models on the entire training dataset.

---

### 7. **Evaluation**

- Evaluate models on:
  - Training data

<img width="172" height="41" alt="image" src="https://github.com/user-attachments/assets/58782cab-fe0a-4776-bafb-efe67245f5b3" />

  - Test data (`test.csv` with labels from `gender_submission.csv`)

    <img width="167" height="36" alt="image" src="https://github.com/user-attachments/assets/ccdec5b8-ca68-4373-88c8-6c847e710ec0" />


- Metrics:
  - Accuracy
  - Precision
  - Recall
  - Confusion matrix (visualized using heatmaps for Logistic Regrission:)
    

    <img width="227" height="75" alt="image" src="https://github.com/user-attachments/assets/c9e21d90-2f25-4c15-a282-0069099f1766" />

    
<img width="574" height="472" alt="image" src="https://github.com/user-attachments/assets/026e7516-324c-41f1-b5f2-5a144840e2e2" />


- Confusion matrix (visualized using heatmaps for RandomForest:)

  
    <img width="265" height="100" alt="image" src="https://github.com/user-attachments/assets/66314b20-4871-4419-a3fa-8bf654d55378" />

 
<img width="575" height="491" alt="image" src="https://github.com/user-attachments/assets/b3312838-e808-47d7-a01a-436adda8a23f" />








---

### 8. **Hyperparameter Tuning**

- Use **RandomizedSearchCV** to tune Logistic Regression:
  - Parameter grid:
    - `C`: 20 values between 10^-0.9 and 10^0.9 (logarithmic scale)
    - `solver`: `liblinear`
  - Perform 5 iterations with 5-fold cross-validation.
- Output:
  - Best hyperparameters

    <img width="412" height="32" alt="image" src="https://github.com/user-attachments/assets/348f7bd4-11c1-4948-aea0-3355549fb6ea" />


  - Best cross-validation score

    <img width="156" height="22" alt="image" src="https://github.com/user-attachments/assets/78d6180d-a619-45a7-928a-089a30797d66" />


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
