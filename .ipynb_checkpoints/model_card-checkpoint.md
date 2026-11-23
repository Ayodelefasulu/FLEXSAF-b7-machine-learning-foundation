# Model Card: Student Performance Classification

## 1. Model Overview

- **Project name:** Student Performance Classification
- **Model name:** Decision Tree Classifier
- **Model type:** Decision Tree (supervised machine learning)
- **Machine learning task:** Binary classification
- **Framework:** Scikit-learn
- **Model version:** Version 1.0 (initial experimental model)

## 2. Intended Use

- **Intended purpose:** To predict whether a student's examination score will be at least 68 based on selected academic and behavioural features.
- **Intended users:** Students, machine learning learners, educators and researchers interested in understanding and experimenting with student performance prediction.
- **Out-of-scope uses:** The model is not intended for making admission, grading, disciplinary, scholarship or other high-impact educational decisions. It should not be used as a substitute for teachers' assessments or official academic evaluation procedures.

## 3. Dataset Information

- **Dataset name:** StudentPerformanceFactors.csv
- **Dataset source:** Kaggle dataset (original source and dataset URL should be verified and recorded).
- **Number of records:** 6,607
- **Number of input features:** 5
- **Target variable:** High_Score
- **Target definition:** A binary variable derived from Exam_Score. A value of 1 represents an examination score greater than or equal to 68, while a value of 0 represents a score below 68.

Target creation:

```python
df["High_Score"] = (df["Exam_Score"] >= 68).astype(int)
```

Target distribution:

| Class | Description | Records | Percentage |
|---|---|---:|---:|
| 0 | Score below 68 | 3,599 | 54.47% |
| 1 | Score at least 68 | 3,008 | 45.53% |
| **Total** | | **6,607** | **100%** |

The threshold of 68 was selected for this educational classification exercise. It does not represent an official academic pass mark.

## 4. Features

The model uses the following five numerical input features:

1. **Hours_Studied:** Number of hours spent studying.
2. **Attendance:** Student attendance measure.
3. **Previous_Scores:** Student's previous examination scores.
4. **Sleep_Hours:** Number of hours spent sleeping.
5. **Tutoring_Sessions:** Number of tutoring sessions attended.

The Exam_Score column was excluded from the input features because it was used to create the target variable. Including it would introduce target leakage.

## 5. Training Configuration

- **Training/testing split:** 80% training and 20% testing.
- **Random state:** 42.
- **Stratification:** Enabled using `stratify=y` to preserve the target class proportions in both datasets.
- **Algorithm:** Scikit-learn DecisionTreeClassifier.
- **Criterion:** Gini impurity.
- **Other algorithm parameters:** Default Scikit-learn settings.
- **Training records:** 5,285.
- **Testing records:** 1,322.

Model configuration:

```python
from sklearn.tree import DecisionTreeClassifier

dt_model = DecisionTreeClassifier(
    criterion="gini",
    random_state=42
)

dt_model.fit(X_train, y_train)
```

## 6. Evaluation Results

The model was evaluated using the test dataset containing 1,322 observations.

| Evaluation metric | Result |
|---|---:|
| Accuracy | 78.82% |
| Precision | 76.14% |
| Recall | 77.91% |
| F1-score | 77.01% |
| ROC-AUC | Not yet calculated |

### Confusion Matrix

| | Predicted 0 | Predicted 1 |
|---|---:|---:|
| Actual 0 | 573 | 147 |
| Actual 1 | 133 | 469 |

Interpretation:

- **True Negatives (573):** Students correctly classified as scoring below 68.
- **False Positives (147):** Students predicted to score at least 68 but whose actual scores were below 68.
- **False Negatives (133):** Students predicted to score below 68 but whose actual scores were at least 68.
- **True Positives (469):** Students correctly classified as scoring at least 68.

The model achieved an accuracy of approximately 78.82%, meaning it correctly classified 1,042 out of 1,322 test observations.

Precision of 76.14% indicates that approximately 76% of positive predictions were correct, while recall of 77.91% indicates that the model identified approximately 78% of the actual positive cases.

## 7. Limitations

The model has several limitations:

1. **Dataset limitation:** The model was trained using one dataset containing 6,607 records. Its performance on students from other schools, regions or educational systems has not been established.

2. **Target limitation:** The classification threshold of 68 was selected for educational experimentation and is not based on an established academic grading policy.

3. **Feature limitation:** The model uses only five numerical features. Other potentially relevant factors, including parental involvement, access to learning resources, teacher quality and family income, were excluded.

4. **Generalisation limitation:** Evaluation was conducted using a single stratified train/test split. Cross-validation and testing on independent external datasets have not yet been performed.

5. **Model limitation:** Decision Trees can overfit training data, particularly when tree depth and other complexity parameters are not restricted.

6. **Prediction limitation:** The model produces predictions based on statistical patterns in the training data. Its predictions are not guaranteed to represent actual future examination outcomes.

7. **Interpretability limitation:** Feature importance indicates how features contributed to the model's predictions but does not establish causal relationships.

## 8. Ethical Considerations

The model may reflect biases or limitations present in its training dataset. If the dataset does not adequately represent different student populations, its predictions may be less reliable for some groups.

The model should be used responsibly and primarily for educational experimentation and machine learning research.

Its predictions should not be used as the sole basis for decisions affecting students' academic opportunities, admissions, scholarships, disciplinary actions or educational placement.

The model should not be interpreted as a definitive measure of a student's intelligence, ability or future academic potential.

Further validation, bias assessment and consultation with relevant educational stakeholders would be necessary before considering any real-world application.

## 9. Reproducibility

- **Programming language:** Python.
- **Python version:** To be confirmed from the development environment.
- **Scikit-learn version:** To be confirmed.
- **Pandas version:** To be confirmed.
- **Other dependencies:** NumPy, Matplotlib and Jupyter Notebook.
- **Dataset:** StudentPerformanceFactors.csv.

### Instructions for running the project

1. Clone or download the project repository.
2. Install the dependencies listed in `requirements.txt`.
3. Place the dataset in the project's `data/` directory.
4. Open the Jupyter Notebook.
5. Execute the notebook cells in order, starting with dataset loading and preparation.
6. Create the target variable and select the input features.
7. Split the dataset into training and testing sets using the documented configuration.
8. Train the Decision Tree Classifier.
9. Generate predictions and evaluate the model using the documented metrics.

To inspect the installed package versions:

```python
import sys
import sklearn
import pandas as pd
import numpy as np
import matplotlib

print("Python:", sys.version)
print("Scikit-learn:", sklearn.__version__)
print("Pandas:", pd.__version__)
print("NumPy:", np.__version__)
print("Matplotlib:", matplotlib.__version__)
```

## 10. Conclusion

The Student Performance Classification project demonstrates the application of supervised machine learning to a binary classification problem.

A Decision Tree Classifier was trained using five numerical student-related features to predict whether an examination score would be below 68 or at least 68.

The model achieved 78.82% accuracy, 76.14% precision, 77.91% recall and a 77.01% F1-score on the test dataset.

The exercise demonstrates the fundamental machine learning workflow, including data preparation, feature selection, target definition, train/test splitting, model training, prediction and performance evaluation.

Before considering real-world deployment, further work would be required, including cross-validation, hyperparameter optimisation, comparison with alternative algorithms, evaluation on independent datasets, bias assessment and improved validation of the target definition.

The model should currently be regarded as an educational machine learning experiment rather than a validated educational prediction system.