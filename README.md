"Student Exam Score Prediction — Haystek Assessment"

This project is an end-to-end Machine Learning pipeline designed to predict Math exam scores using student demographic, socioeconomic, and academic features.
It demonstrates a complete workflow: EDA → Preprocessing → Modeling → Hyperparameter Tuning → Deployment (Pickle Model).

This assignment is submitted as part of the Haystek Technologies Round-2 Machine Learning Assessment.




* Objective :
Build a complete ML solution that predicts MathScore for a student based on historical data and multiple influencing factors.




* Dataset Description
Two datasets were provided:

* Original_data_with_more_rows.csv
30,641 rows
8 columns
No missing values
Suitable for quick data understanding

* Expanded_data_with_more_features.csv
30,641 rows
14 columns
Contains missing values
Ideal for ML tasks
Used for the entire modeling process




* Target variable:
MathScore

* Removed to avoid leakage:
ReadingScore
WritingScore




** Project Workflow :
1. Data Exploration :
- Checked missing values
- Performed descriptive statistics
- Visualized distributions of Math/Reading/Writing scores
- Observed strong correlation between Reading ⇄ Writing ⇄ Math → Led us to drop them as predictors (to prevent leakage)
- Identified categorical vs numerical features

2️. Data Preprocessing :
Implemented a scikit-learn ColumnTransformer:

- Numerical Features :
Imputed using median
Scaled using StandardScaler

- Categorical Features :
Imputed using most_frequent
Encoded using OneHotEncoder(handle_unknown="ignore")

The pipeline ensures clean, consistent, and reproducible data processing.

3️. Train–Test Split :
80% training
20% testing
random_state=42 for reproducibility

4️. Modeling :
Two models were trained:

* Linear Regression (Baseline Model)
Interpretable
Fast to train
Used to establish benchmark performance

* Random Forest Regressor
Capable of capturing nonlinear relationships
Tunable
More robust

Both models were built inside a pipeline to ensure preprocessing is applied consistently.

5️. Model Evaluation

Metrics used:

MAE (Mean Absolute Error)
RMSE (Root Mean Squared Error)
R² Score

- Linear Regression Results
MAE  : 10.383
RMSE : 12.840
R²   : 0.289

- Random Forest (Before Tuning)
MAE  : 11.560
RMSE : 14.360
R²   : 0.111


* Observation:
Random Forest underperformed initially due to untuned hyperparameters.

6️. Hyperparameter Tuning :
Performed using RandomizedSearchCV with 3-fold cross-validation.

Best parameters found:

n_estimators    = 200
max_depth       = 10
min_samples_split = 10
min_samples_leaf  = 1
max_features      = 'sqrt'

📊 Tuned Random Forest Results
MAE  : 10.498
RMSE : 12.980
R²   : 0.274

* Observation:
Model performance improved significantly after tuning, nearly matching Linear Regression.


7️. Final Model Deployment
The final model (pipeline + preprocessing + trained algorithm) was saved using pickle:
student_exam_mathscore_model.pkl

A prediction function was created to accept new student data and produce a MathScore prediction.




Example usage:
predict_math_score({
    "Gender": "female",
    "EthnicGroup": "group B",
    "ParentEduc": "some college",
    "LunchType": "standard",
    "TestPrep": "none",
    "ParentMaritalStatus": "married",
    "PracticeSport": "sometimes",
    "IsFirstChild": "yes",
    "NrSiblings": 2,
    "TransportMeans": "school_bus",
    "WklyStudyHours": "5 - 10"
})




* Project Structure
haystek_assessment/
│
├── data/
│   ├── Expanded_data_with_more_features.csv
│   ├── Original_data_with_more_rows.csv
│
├── model/
│   └── student_exam_mathscore_model.pkl
│
├── notebook/
│   └── student_exam_score_prediction.ipynb
│
├── README.md
└── requirements.txt




* How to Run This Project :

1. Create the Conda Environment
conda create -n exam_score_env python=3.10
conda activate exam_score_env

2. Install Dependencies
pip install -r requirements.txt

3. Launch Jupyter Notebook
jupyter notebook

4. Run the notebook cell-by-cell
Located in: notebook/student_exam_score_prediction.ipynb

* Key Insights :
Reading/Writing strongly correlate with Math → removed to avoid leakage
Categorical features significantly influence model performance
Linear Regression surprisingly outperformed initial Random Forest
Hyperparameter tuning drastically improved Random Forest
R² remained moderate → indicates students’ scores depend on many external factors not captured in dataset
