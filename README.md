# Cybersecurity Intrusion Detection Analysis

This repository contains a Jupyter Notebook (`main.ipynb`) that performs a comprehensive analysis and builds machine learning models to detect network intrusions from a cybersecurity dataset.

The project walks through the entire data science workflow:
1.  **Data Loading and Cleaning**
2.  **Exploratory Data Analysis (EDA)**
3.  **Feature Importance and Selection**
4.  **Model Training and Comparison**
5.  **Interactive Prediction**

## 📂 Project Workflow

The `main.ipynb` notebook is structured as follows:

### 1. Data Loading and Cleaning
* Loads the `cybersecurity_intrusion_data.csv` dataset.
* Checks for and removes any duplicate rows.
* Checks for and removes any rows containing null (NaN) values.

### 2. Exploratory Data Analysis (EDA)
The notebook investigates patterns in the data to understand the characteristics of an attack:
* **Protocol Type:** A stacked bar chart shows the count of normal vs. intrusion events for each protocol (TCP, UDP, ICMP).
* **Browser Type:** A bar chart visualizes the intrusion *rate* (%) by browser.
* **Login Attempts:** A table compares the average `login_attempts` and `failed_logins` for both normal and intrusion sessions.

### 3. Feature Importance
* A **Random Forest Classifier** is used to determine the most predictive features for detecting an attack.
* A correlation matrix heatmap is generated to visualize the relationships between numerical features and the `attack_detected` target.

### 4. Model Training and Evaluation
Three different classification models are trained and evaluated to find the best performer:
1.  **Random Forest Classifier**
2.  **Logistic Regression**
3.  **Gaussian Naive Bayes**

The models are compared using:
* **Classification Reports:** Detailed precision, recall, and F1-scores for both "Normal" and "Intrusion" classes.
* **Comparison Chart:** A bar chart comparing the overall Accuracy, Precision (for intrusion), Recall (for intrusion), and F1-Score (for intrusion) across all three models.
* **Confusion Matrices:** A side-by-side plot of the confusion matrices for each model to visualize true/false positives and negatives.

### 5. Interactive Prediction
The notebook concludes with a simple function (`predict_user_input`) that allows you to enter session details manually and receive a real-time intrusion prediction from the trained model.

## 📊 Key Findings

* **Top Features:** The most important features for predicting an intrusion, according to the Random Forest model, are:
    1.  `failed_logins` (Importance: 0.286)
    2.  `ip_reputation_score` (Importance: 0.233)
    3.  `login_attempts` (Importance: 0.215)

* **Browser Risk:** Sessions originating from an **'Unknown'** browser have a significantly higher intrusion rate (73.6%) compared to known browsers like Chrome or Firefox (which are around 42-43%).

* **Model Performance:** The **Random Forest Classifier** was the clear winner, demonstrating the best balance of precision and recall for detecting intrusions.

| Model | Accuracy | F1-Score (Intrusion) |
| :--- | :---: | :---: |
| **Random Forest** | **0.90** | **0.87** |
| Naive Bayes | 0.83 | 0.78 |
| Logistic Regression | 0.73 | 0.69 |

## 🚀 How to Run

### 1. Clone the Repository
```bash
git clone [https://github.com/your-username/cybersecurity-intrusion-detection.git](https://github.com/your-username/cybersecurity-intrusion-detection.git)
cd cybersecurity-intrusion-detection
