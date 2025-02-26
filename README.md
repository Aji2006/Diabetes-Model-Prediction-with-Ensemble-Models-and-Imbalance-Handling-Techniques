# **Diabetes Model Prediction with Ensemble Models and Imbalance Handling Techniques**

## Overview 
This repository presents a comprehensive study on predicting diabetes using a clinical dataset containing 100,000 samples. The dataset includes detailed health and demographic information—such as gender, age, location, race, hypertension, heart disease, smoking history, BMI, HbA1c level, blood glucose level, and diabetes status—making it ideal for predictive modeling, health analytics, and clinical research.

## Dataset
The "Diabetes Clinical Dataset (100k rows)" provides extensive insights into patient health and demographics. It is designed for multiple use cases:
  - Predictive Modeling: Building models to predict the likelihood of diabetes.
  - Health Analytics: Analyzing correlations between health metrics (e.g., BMI, HbA1c) and diabetes.
  - Clinical Research: Identifying risk factors and exploring demographic trends in diabetes prevalence.

## Models Evaluated
Four classification models have been developed and evaluated:
  - AdaBoost
  - XGB (XGBoost)
  - Random Forest (RF)
  - LGBM Classifier (LightGBM)
These models were trained and tested under two scenarios:
  1. Without Imbalance Techniques
  2. With Imbalance Techniques, using the following methods:
     - ADASYN
     - SMOTE
     - Random Undersampler

## Experiment and Results
1. Without Imbalance Techniques
  - Training/Testing Scores:
      - AdaBoost: ~0.9718 / 0.9723
      - XGB: ~0.9772 / 0.9713
      - Random Forest: ~1.0000 / 0.9724
      - LGBM: ~0.9390 / 0.9264
  - Observations:
      - Although overall accuracy is high (around 97%) for AdaBoost, XGB, and RF, the models struggle to correctly classify the minority class (diabetes-positive). For instance, AdaBoost exhibits a recall of only 0.67 for the diabetes class.
      - LGBM, in particular, shows very low precision (0.54) for the minority class despite a relatively high recall (0.88).
  - Interpretation: High overall accuracy masks a critical issue: the inability to effectively detect the minority class, which is essential in medical diagnosis.
2. With Imbalance Techniques
   A. ADASYN
      - XGB, RF, and LGBM: Maintained high testing scores (~0.968–0.971) with improved class balance and macro f1-scores approaching 0.89.
      - AdaBoost: Although the recall for the minority class increased (up to 0.88), precision dropped significantly (around 0.44), leading to a lower overall f1-score and testing score (~0.893).
   B. SMOTE
      - Similar improvements as ADASYN were observed for XGB, RF, and LGBM, with testing scores near 0.97 and balanced metrics.
      - AdaBoost’s performance improved slightly but remained less consistent compared to the other models.
   C. Random Undersampler
      - This method led to a notable drop in performance for all models, with testing scores around 0.90 and macro f1-scores in the range of 0.77–0.78.
      - The significant reduction in training data appears to remove critical information, thus degrading model performance.
   - Interpretation: Oversampling techniques (ADASYN and SMOTE) are effective at enhancing minority class detection without sacrificing overall accuracy—especially for XGB, RF, and LGBM. In contrast, random undersampling is less effective due to the loss of valuable training data.

## Overall Conclusion
- Without Imbalance Techniques: Despite high overall accuracy, the models are not adequately identifying diabetes-positive cases, as demonstrated by low recall and f1-scores for the minority class.
- Recommended Approach: Oversampling methods such as SMOTE or ADASYN are highly recommended, particularly when combined with XGB, Random Forest, or LGBM. These approaches yield testing scores around 0.97 and improve the balance between sensitivity (recall) and precision for the minority class.
- Not Recommended: Random undersampling consistently results in lower performance due to the significant loss of training data.

## Repository Structure
  - data/: Contains the dataset or instructions for downloading it.
  - notebooks/: Jupyter notebooks that document the exploratory data analysis (EDA), model training, evaluation, and experiments with imbalance handling techniques.
  - src/: Source code for data preprocessing, model training, and evaluation scripts.
  - README.md: This file with an overview of the project.
