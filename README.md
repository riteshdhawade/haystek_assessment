**Student Exam Score Prediction**

**Haystek Technologies – Machine Learning Assessment**

**Project Overview**

This project implements an end-to-end machine learning pipeline to predict student MathScore based on demographic, socioeconomic, and academic features. The workflow includes exploratory data analysis, data preprocessing, model development, model evaluation, hyperparameter tuning, and deployment through a serialized model file.

The objective is to build an accurate and reproducible prediction system that can generalize to new student profiles.

**Dataset Information**

Two datasets were provided with identical row counts but different feature sets.

1. Original dataset

Contains eight columns
No missing values
Used for initial inspection

2. Expanded dataset

Contains fourteen columns
Includes several categorical and numerical features
Contains missing values
Used for the entire modeling process

MathScore is the prediction target. ReadingScore and WritingScore were excluded from training to prevent data leakage due to strong correlation with MathScore.

**Methodology**

**1. Exploratory Data Analysis**

The dataset was inspected for structure, types, value distributions, missing values, and correlations. Score distributions were analyzed, and relationships between subjects were examined. Strong correlation between ReadingScore, WritingScore, and MathScore justified removing the reading and writing scores from the feature set.

**2. Data Preprocessing**

A preprocessing pipeline was created using a ColumnTransformer. The following steps were applied:

Missing values in numerical features were imputed using median values.

Missing values in categorical features were imputed using the most frequent category.

Numerical features were standardized.

Categorical features were one-hot encoded.

This pipeline ensures consistent transformation during both training and prediction.

**3. Train–Test Split**

The dataset was divided into an 80 percent training set and a 20 percent testing set to evaluate model performance on unseen data. The split ensures fair assessment of generalization ability.

**4. Model Development**

Two regression models were trained:

Linear Regression (baseline model)

Random Forest Regressor (ensemble model)

Both models were wrapped inside a pipeline that included all preprocessing steps. This ensures the model receives clean and encoded features consistently.

**5. Model Evaluation**

Models were evaluated on the test set using mean absolute error, root mean squared error, and the coefficient of determination.

Summary of key results:

Linear Regression achieved the best overall performance with the lowest error values and the highest R² score.

The initial Random Forest model underperformed due to default hyperparameters.

**6. Hyperparameter Tuning**

RandomizedSearchCV was used to improve the Random Forest model. Various parameters related to tree depth, number of estimators, minimum samples required for splitting, and feature selection were tuned.

The tuned model showed significant improvement, reducing error metrics and increasing the R² score. However, Linear Regression remained the best-performing model for this dataset.

**7. Model Deployment**

The final selected model (Linear Regression) was serialized using the pickle library. A prediction function was implemented to:

Load the saved model

Accept new student records in dictionary format

Transform the data using the internal preprocessing pipeline

Output predicted MathScore

This completes an end-to-end deployment-ready workflow.

**Project Structure**

The repository follows a structured layout for clarity:

project-root/
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

**Key Insights**

Several categorical and demographic factors influence student performance.

Weekly study hours, test preparation, parental education level, and lunch type showed meaningful associations with performance.

ReadingScore and WritingScore were intentionally excluded to avoid leakage because they strongly predict MathScore.

Linear Regression provided strong baseline performance, indicating largely linear relationships in the dataset.

Hyperparameter tuning improved the Random Forest model but did not surpass Linear Regression.

**Conclusion**

The project successfully demonstrates:

A complete machine learning workflow

Systematic data cleaning and preprocessing

Comparison of multiple models

Hyperparameter tuning

Deployment of a reusable prediction model

This pipeline is ready for practical use and can be extended with additional features, domain data, or more advanced regression techniques if required.
