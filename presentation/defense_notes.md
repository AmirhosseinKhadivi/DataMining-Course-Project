# Defense Notes

## Project Summary

This project performs multiclass classification on the Heart Disease
dataset. The target contains five classes from 0 to 4.

## Important Numbers

- Dataset rows: 920
- Original columns: 16
- Training rows: 736
- Test rows: 184
- Train-test ratio: 80/20
- Random state: 42
- Cross-validation folds: 5
- Recommended algorithm: KNN
- Recommended Macro F1: 0.4172

## Common Defense Questions

### 1. Why was the ID column removed?

The ID column identifies records and does not represent a medical
feature. Including it could create meaningless patterns.

### 2. Why was stratification used?

The target classes are imbalanced. Stratification preserves similar
class proportions in the training and test sets.

### 3. Why is accuracy not sufficient?

A model can obtain acceptable accuracy by focusing on the majority
class. Macro F1 gives equal importance to every target class.

### 4. Why was Macro F1 the primary metric?

The dataset contains five imbalanced classes. Macro F1 evaluates each
class equally before calculating the average.

### 5. What is data leakage?

Data leakage occurs when information from validation or test data
influences model training. All imputers, encoders, and scalers were
fitted only on training data.

### 6. Why was a Pipeline used?

The Pipeline combines preprocessing and classification. It ensures that
the same transformations are applied consistently and prevents leakage
during cross-validation.

### 7. Why were suspicious zeros replaced?

Zero blood pressure and zero cholesterol were treated as unavailable
measurements based on a rule-based data-quality assumption.

### 8. What is the difference between Linear and RBF SVM?

Linear SVM creates linear decision boundaries. RBF SVM can model
nonlinear class relationships.

### 9. Why does KNN require scaling?

KNN uses distance calculations. Features with larger numeric scales can
dominate the distance without scaling.

### 10. Why does Decision Tree not require scaling?

Decision Trees split features using thresholds. Their decisions are not
based on geometric distance.

### 11. What does class weight balanced do?

It assigns greater importance to minority classes and lower importance
to majority classes based on their frequencies.

### 12. Why was the dataset feature tested both ways?

The dataset column identifies collection centers. It may improve
performance but can also cause the model to learn source-specific
patterns.

### 13. Why was temporal analysis not performed?

The dataset contains no valid date or time feature. The dataset source
column is not a temporal variable.

### 14. What does a Confusion Matrix show?

It shows the number of correct and incorrect predictions for every
actual and predicted class combination.

### 15. Why was the test set evaluated only after model selection?

Repeatedly selecting models based on test performance would make the
test set part of the training decision process.

## Final Recommendation

The selected model is KNN with a test Macro F1 of
0.4172, balanced accuracy of
0.3997, and class 4 recall of
0.1667.
