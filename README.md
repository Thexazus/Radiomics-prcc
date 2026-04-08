# Radiomics for classification prcc vs non prcc

## Description
Renal tumor classification is challenging due to similar imaging features. This study uses radiomics from CT scans (KiTS19) with feature selection (RFE, RF importance) and ML models (XGBoost, RF, LR). Logistic Regression + RFE performed best (89.8%), highlighting the importance of feature selection for accurate, non-invasive diagnosis.

## Dataset Information
* **Final Dataset (2-Class):** (https://www.kaggle.com/datasets/audreygrcia/kits19-papillary-nonpapillary/versions/1)
- Total samples: 49 patients 
- Features: ~740 radiomic features
- Classes:
  - Papillary
  - Non-Papillary (Chromophobe + Oncocytoma)

* * **Preliminary Dataset (6-Class):** )https://kits19.grand-challenge.org/data/)

 
## Code Information
The implementation utilizes a radiomics-based machine learning pipeline designed for the classification of renal tumors (Papillary vs Non-Papillary) from CT scan data. The framework employs a stacking ensemble approach combining Random Forest and Logistic Regression to balance non-linear pattern recognition and linear generalization.

Model interpretability is implicitly supported through the use of Logistic Regression, which provides stable global feature relationships, while Random Forest captures complex interactions among radiomic features such as texture (GLCM, GLRLM) and intensity-based descriptors.


## Usage Instructions
1. **Dataset Preparation** : Prepare the radiomics dataset containing extracted features (e.g., shape, first-order statistics, texture features such as GLCM and GLRLM). Ensure the dataset is labeled into: Papillary, Non-Papillary (Chromophobe + Oncocytoma)
2. **Environment Setup**:
Ensure Python 3.x is installed and all dependencies listed in the Requirements section are satisfied.
3. **Training**:
Run the training script to perform preprocessing, feature selection, and model training using the stacking approach.
4. **Evaluation**:
Evaluate the trained model using classification metrics such as accuracy, precision, recall, and F1-score.

## Requirements
To set up the environment, install the following dependencies:
pip install numpy pandas scikit-learn matplotlib seaborn

## Methodology (Data Processing & Modeling)
1. **Preprocessing** : To address the high-dimensional and small-sample nature of the radiomics dataset (p >> n), the following steps were applied:
-Feature Selection : Reduces dimensionality and removes redundant radiomic features to prevent overfitting.
-Feature Scaling : StandardScaler is applied to normalize feature distributions and ensure comparable feature ranges.
-Class Balancing: Data filtering was performed to reduce class imbalance, resulting in a subset of 33 patients.

2.**Model Architecture** : A stacking ensemble framework was implemented to improve generalization performance:
-Base Learners:
Random Forest: Captures non-linear interactions and complex feature combinations.
Logistic Regression: Captures global linear relationships and provides stable predictions.
-Meta Learner:
Logistic Regression: Combines predictions from base learners to produce the final classification.

This combination is motivated by the need for model diversity, where linear and non-linear models provide complementary learning representations.

3. **Design Considerations**

The choice of combining Random Forest and Logistic Regression instead of multiple tree-based models (e.g., Random Forest and XGBoost) is based on the following considerations:

Tree-based models tend to produce highly correlated predictions when applied to high-dimensional radiomics data.
Boosting methods such as XGBoost may amplify noise in small datasets, increasing the risk of overfitting.
Combining linear and non-linear models improves diversity in stacking and enhances generalization capability.

## Materials & Methods
**Dataset Description**
Total Samples: 49 patients (filtered to 33 for balanced classification)
Features: ~740 radiomic features
Classes:Papillary, Non-Papillary (Chromophobe + Oncocytoma)

**Computing Infrastructure**
Operating System: Windows / macOS / Linux
Python Version: 3.x
Hardware: Standard CPU (no GPU required)
Evaluation Method

The system was evaluated using the following approach:

**Training Strategy**:
Model training was conducted using a structured pipeline including preprocessing, feature selection, and stacking-based classification.
Performance Metrics:
Accuracy
Precision
Recall
F1-score
**Generalization Analysis**:
Special attention was given to overfitting due to the high feature-to-sample ratio. The stacking approach was designed to improve robustness on unseen data.
Notes on Limitations
The dataset size is relatively small, which may affect model generalization.
Radiomic features may contain redundancy and high correlation.
Results may vary depending on feature selection strategy and random seed.
