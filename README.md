# ChurnGuard: End-to-End Customer Churn Prediction

ChurnGuard is an end-to-end machine learning project designed to predict customer churn for telecommunications services. By analyzing customer usage patterns, contract structures, and billing details, the pipeline preprocesses data, trains a classification model, and provides a command-line interface to test individual customer retention risks in real time.

---

## Project Structure

```text
ChurnGuard/
│
├── task1_load_explore.py          # Data ingestion, schema inspection, and exploratory data checks
├── task2_clean_data.py            # Data cleaning, type conversion, outlier filtering, and imputation
├── task3_train_model.py           # Feature encoding, train/test split, model training, and evaluation
├── task4_predict.py               # Interactive CLI for single-customer churn inference
│
├── churn_prediction_model.pkl     # Serialized Scikit-Learn Logistic Regression model
├── churn_prediction_features.pkl  # Pickled list of 20 feature column names used during training
└── logistic_regression_report.txt # Accuracy and classification metrics on the test dataset

```
## ⚙️ How It Works (Step-by-Step)

The project follows a simple 4-step machine learning pipeline:

---

### Step 1: Explore the Data (`task1_load_explore.py`)
Before building anything, we inspect the raw dataset (`churnguard_data.csv`):
* **Check Data Health:** Looks for missing values and duplicate rows.
* **Understand the Target:** Checks how many customers churned vs. stayed.
* **Inspect Columns:** Reviews data types and unique entries across categories.

---

### Step 2: Clean the Data (`task2_clean_data.py`)
Prepares raw records so the model can read them properly:
* **Remove Clutter:** Drops `customerID` (doesn't help predict churn) and duplicate entries.
* **Fix Text & Formatting:** Trims extra spaces and standardizes lowercase/uppercase text.
* **Handle Bad Numbers:** Converts `TotalCharges` to numbers and filters out invalid tenures ($\le 0$).
* **Fill in Blanks:** Imputes missing numerical fields using the column mean or median.
* **Save Clean Data:** Exports the finished file as `churnguard_clean.csv`.

---

### Step 3: Train the Model (`task3_train_model.py`)
Teaches the machine learning algorithm to spot churn patterns:
* **Encode Categories:** Converts text labels (like "Yes"/"No" and contract types) into 0s and 1s.
* **Split the Data:** Keeps 80% for training and saves 20% to test accuracy on unseen data.
* **Train Logistic Regression:** Fits a classification model using Scikit-Learn.
* **Save the Results:**
  * Stores test scores in `logistic_regression_report.txt`.
  * Saves the trained model to `churn_prediction_model.pkl`.
  * Saves the feature names to `churn_prediction_features.pkl` for future use.

---

### Step 4: Make Live Predictions (`task4_predict.py`)
An interactive terminal tool to test new customer profiles in real time:
* **Ask for Input:** Prompts you to enter tenure, charges, contract type, and senior status.
* **Align Features:** Formats your answers to match the model's exact expectations.
* **Display Verdict:** Instantly outputs **Likely to CHURN** or **Likely to STAY**.
