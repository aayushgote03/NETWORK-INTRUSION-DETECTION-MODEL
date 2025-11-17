Here is an attractive `README.md` file for your GitHub project, based on the code and analysis from your Jupyter Notebook.

It's structured to clearly explain the project's purpose, workflow, and results, making it perfect for a portfolio.

-----

# Cybersecurity Attack Detection Model

This project uses machine learning to classify network sessions as "Normal" or "Intrusion." It's based on a sample cybersecurity dataset and demonstrates a complete ML workflow, from exploratory data analysis (EDA) to model comparison and robust performance evaluation.

## 🚀 Project Workflow

This notebook follows a systematic approach to model development:

1.  **Exploratory Data Analysis (EDA):** Analyzed the dataset to understand feature distributions, class balance, and correlations.
2.  **Preprocessing:** Built a `ColumnTransformer` pipeline to scale numeric features (`StandardScaler`) and encode categorical features (`OneHotEncoder`).
3.  **Model Selection:** Trained and compared four different classification models:
      * Logistic Regression
      * K-Nearest Neighbors (KNN)
      * Random Forest
      * Gaussian Naive Bayes
4.  **Performance Evaluation:** Used three different methods to ensure a robust and reliable measure of each model's performance:
      * 5-Fold Cross-Validation
      * 100-Iteration Bootstrapping (with Out-of-Bag accuracy)
      * Final evaluation on a hold-out test set (20% of data).
5.  **Interactive Prediction:** Created a function to run predictions on new, unseen data using the trained models.

## 📊 Exploratory Data Analysis (EDA)

The analysis revealed several key insights:

  * **Class Balance:** The dataset is fairly balanced, with approximately 54% "Normal" sessions and 46% "Intrusion" sessions.
  * **Correlations:** `failed_logins` and `login_attempts` are strongly correlated. `ip_reputation_score` and `failed_logins` show the strongest correlation with the target variable, `attack_detected`.
  * **Categorical Features:** `protocol_type` (UDP) and `browser_type` (Unknown) showed a noticeable association with intrusion attempts.

## 🏆 Model Comparison & Results

To find the best model, all four algorithms were rigorously tested using cross-validation and bootstrapping on the training data.

### 1\. 5-Fold Cross-Validation

Random Forest showed the highest and most stable accuracy.

| Model | Mean\_Accuracy | Std\_Dev |
| :--- | :--- | :--- |
| **Random Forest** | **0.869** | 0.070 |
| Logistic Regression | 0.769 | 0.083 |
| Naive Bayes | 0.713 | 0.064 |
| K-Nearest Neighbors (KNN) | 0.688 | 0.044 |

### 2\. Bootstrapping (100 Iterations)

Bootstrapping confirmed the Random Forest's superior performance and stability (lowest standard deviation).

| Model | Mean OOB Accuracy | Std\_Dev |
| :--- | :--- | :--- |
| **Random Forest** | **0.837** | 0.047 |
| Logistic Regression | 0.750 | 0.052 |
| K-Nearest Neighbors (KNN) | 0.666 | 0.052 |
| Naive Bayes | 0.650 | 0.093 |

### 3\. Final Test Set Evaluation

The models were retrained on the full training set (160 samples) and evaluated one final time on the 40-sample hold-out test set. The Random Forest model again achieved the highest accuracy at **78%**.

## 💡 Interactive Prediction

The notebook includes a `predict_intrusion` function to test new data. It accepts a dictionary and returns a prediction and probability score from all four models.

### Example: Suspicious Session

```python
# --- Example 1: Simulating a suspicious session ---
suspicious_session = {
    'failed_logins': 3,
    'ip_reputation_score': 0.75, # High
    'login_attempts': 4,
    'session_duration': 10.5, # Very short
    'network_packet_size': 800,
    'browser_type': 'Unknown',
    'protocol_type': 'UDP',
    'unusual_time_access': 1, # Unusual
    'encryption_used': 'DES'
}
predict_intrusion(suspicious_session)
```

**Output:**

```
--- Input Data ---
 network_packet_size  login_attempts  session_duration  ip_reputation_score  failed_logins  unusual_time_access protocol_type encryption_used browser_type
                 800               4              10.5                 0.75              3                    1           UDP             DES      Unknown

--- Model Predictions ---
                              Prediction Intrusion Probability
Logistic Regression        **INTRUSION** 99.8%
K-Nearest Neighbors (KNN)  **INTRUSION** 60.0%
Random Forest              **INTRUSION** 89.0%
Naive Bayes                **INTRUSION** 100.0%
```

### Example: Normal Session

```python
# --- Example 2: Simulating a normal session ---
normal_session = {
    'failed_logins': 0,
    'ip_reputation_score': 0.15, # Low
    'login_attempts': 1,
    'session_duration': 1200.0, # Long
    'network_packet_size': 350,
    'browser_type': 'Chrome',
    'protocol_type': 'TCP',
    'unusual_time_access': 0, # Not unusual
    'encryption_used': 'AES'
}
predict_intrusion(normal_session)
```

**Output:**

```
--- Input Data ---
 network_packet_size  login_attempts  session_duration  ip_reputation_score  failed_logins  unusual_time_access protocol_type encryption_used browser_type
                 350               1            1200.0                 0.15              0                    0           TCP             AES       Chrome

--- Model Predictions ---
                          Prediction Intrusion Probability
Logistic Regression           Normal                  1.2%
K-Nearest Neighbors (KNN)     Normal                 40.0%
Random Forest                 Normal                 15.0%
Naive Bayes                   Normal                 49.3%
```

## ⚙️ How to Run

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/your-repo-name.git
    cd your-repo-name
    ```
2.  **Install dependencies:**
    (It's recommended to use a virtual environment)
    ```bash
    pip install -r requirements.txt
    ```
3.  **Run the Jupyter Notebook:**
    ```bash
    jupyter notebook main2.ipynb
    ```

### `requirements.txt`

```
pandas
matplotlib
seaborn
scikit-learn
numpy
jupyter
```
