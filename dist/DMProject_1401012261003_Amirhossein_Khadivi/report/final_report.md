# Final Data Mining Project Report

## Student Information

- Student ID: YOUR_STUDENT_ID
- First Name: YOUR_FIRST_NAME
- Last Name: YOUR_LAST_NAME

## 1. Project Objective

The objective of this project was to preprocess, analyze, and classify
multiclass Heart Disease records. The target variable represents disease
severity using classes 0 through 4.

## 2. Dataset Description

The dataset contains 920 records and 16 original columns. The `id`
column is an identifier and was excluded from machine-learning models.
The `num` column is the multiclass target.

### Target Distribution

| target_class | count | percent |
| --- | --- | --- |
| 0.0 | 411.0 | 44.67 |
| 1.0 | 265.0 | 28.8 |
| 2.0 | 109.0 | 11.85 |
| 3.0 | 107.0 | 11.63 |
| 4.0 | 28.0 | 3.04 |

## 3. Data Quality and Preprocessing

The dataset contains missing values in several numeric and categorical
features.

### Missing-Value Summary

| feature | missing_count | missing_percent | available_count |
| --- | --- | --- | --- |
| ca | 611 | 66.413 | 309 |
| thal | 486 | 52.8261 | 434 |
| slope | 309 | 33.587 | 611 |
| fbs | 90 | 9.7826 | 830 |
| oldpeak | 62 | 6.7391 | 858 |
| trestbps | 59 | 6.413 | 861 |
| exang | 55 | 5.9783 | 865 |
| thalch | 55 | 5.9783 | 865 |
| chol | 30 | 3.2609 | 890 |
| restecg | 2 | 0.2174 | 918 |

The preprocessing workflow included:

1. Replacing suspicious zero values in `trestbps` and `chol` with missing
   values.
2. Comparing mean and median imputation.
3. Representing missing categorical values as an explicit category.
4. Applying One-Hot Encoding to categorical features.
5. Comparing StandardScaler and MinMaxScaler.
6. analyzing outliers using the IQR method.
7. performing all learned preprocessing operations only on training data.

## 4. Exploratory Data Analysis

The exploratory analysis included histograms, KDE plots, skewness,
kurtosis, boxplots, categorical frequency charts, correlation matrices,
feature-target relationships, class imbalance analysis, and dataset
source analysis.

### Main EDA Findings

| finding | feature | value | measurement |
| --- | --- | --- | --- |
| Highest missingness | ca | 66.413 | percent |
| Highest absolute skewness | chol | 1.3149 | absolute_skewness |
| Strongest numeric target correlation | ca | 0.528 | absolute_spearman |
| Strongest numeric target effect | ca | 0.2734 | epsilon_squared |
| Strongest categorical target association | exang | 0.3214 | cramers_v |
| Class imbalance ratio | 0 versus 4 | 14.6786 | majority_to_minority_ratio |
| Total adjusted IQR outliers | continuous_features | 68.0 | count |

No valid temporal column was available. Therefore, temporal trend
analysis was documented as not applicable.

## 5. Data Splitting Strategy

The dataset was divided into 80 percent training data and 20 percent
test data.

Stratification was used to preserve the multiclass target distribution.
The random state was fixed at 42.

## 6. Machine-Learning Models

The following classifiers were evaluated:

- Linear Support Vector Machine
- RBF Support Vector Machine
- K-Nearest Neighbors with multiple neighborhood sizes
- Decision Tree with multiple depth and class-weight configurations

Model configurations were selected using five-fold stratified
cross-validation on the training data.

The test set was used only for final evaluation.

## 7. Evaluation Metrics

The following metrics were calculated:

- Accuracy
- Balanced Accuracy
- Macro Precision
- Macro Recall
- Macro F1
- Weighted F1
- Confusion Matrix
- Per-class Recall

Macro F1 was selected as the primary metric because the target classes
were imbalanced.

## 8. Final Model Comparison

| algorithm | accuracy | balanced_accuracy | macro_precision | macro_recall | macro_f1 | weighted_f1 | class_4_recall |
| --- | --- | --- | --- | --- | --- | --- | --- |
| KNN | 0.5924 | 0.3997 | 0.5665 | 0.3997 | 0.4172 | 0.5782 | 0.1667 |
| RBF SVM | 0.538 | 0.4054 | 0.3998 | 0.4054 | 0.3918 | 0.5657 | 0.1667 |
| Optimized SVM | 0.5054 | 0.4453 | 0.391 | 0.4453 | 0.3818 | 0.5364 | 0.6667 |
| Linear SVM | 0.5054 | 0.4453 | 0.391 | 0.4453 | 0.3818 | 0.5364 | 0.6667 |
| Decision Tree | 0.5598 | 0.3432 | 0.2964 | 0.3432 | 0.3155 | 0.5286 | 0.0 |

## 9. Recommended Model

- Algorithm: KNN
- Accuracy: 0.5924
- Balanced Accuracy: 0.3997
- Macro F1: 0.4172
- Class 4 Recall: 0.1667

The recommended model was selected primarily by Macro F1, followed by
class 4 recall and balanced accuracy.

## 10. Bonus Performance Comparison

The same preprocessing and descriptive-statistics operation was
implemented using raw Python loops and using vectorized Pandas/NumPy
operations.

- Faster method: Pandas and NumPy
- Raw Python to Pandas/NumPy ratio: 9.4112

Vectorized operations were generally faster because they reduce Python
interpreter overhead and use optimized compiled routines.

## 11. Limitations

- The target classes are strongly imbalanced.
- Class 4 contains relatively few observations.
- Missingness differs across dataset collection centers.
- The `dataset` feature may capture source-specific patterns.
- The dataset contains no valid temporal feature.
- Results should not be interpreted as clinical medical advice.

## 12. Conclusion

The project completed the required preprocessing, exploratory analysis,
classification, model comparison, and performance benchmark.

Leakage-safe pipelines were used throughout the modeling workflow.
The final recommendation balances overall performance with performance
on minority classes.
