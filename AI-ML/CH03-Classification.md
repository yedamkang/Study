# Chapter 3: Classification
Hands-On Machine Learning | Date: 2026-09-14 | Author: Yedam Kang

## 1. MNIST

MNIST is a dataset of 70,000 handwritten digit images (0–9). Each image is 28×28 pixels, flattened into a list of 784 numbers (pixel brightness values).

```python
from sklearn.datasets import fetch_openml

# Downloads the MNIST dataset using scikit-learn's built-in function
mnist = fetch_openml('mnist_784', as_frame=False)

X, y = mnist.data, mnist.target
# X: image data (70000 rows, 784 columns)
# y: labels (the actual digit 0-9)

X_train, X_test = X[:60000], X[60000:]
y_train, y_test = y[:60000], y[60000:]
# First 60,000 for training, last 10,000 for testing (pre-split convention)
```

## 2. Training a Binary Classifier

We train a model that only answers "Is this a 5, or not?"

```python
from sklearn.linear_model import SGDClassifier

# Convert labels into True/False: "is it a 5?"
y_train_5 = (y_train == '5')
y_test_5 = (y_test == '5')

sgd_clf = SGDClassifier(random_state=42)
# random_state=42: fixes randomness so results are reproducible (42 is just a common convention)

sgd_clf.fit(X_train, y_train_5)
# train the model

sgd_clf.predict([X_train[0]])
# predict whether the first image is a 5
```

## 3. Performance Measures

Accuracy alone is misleading (if only 10% of digits are 5, guessing "not 5" always still gives 90% accuracy). So we use multiple metrics together.

```python
from sklearn.model_selection import cross_val_score
# Cross-validation: splits data into folds, tests multiple times to avoid lucky results
cross_val_score(sgd_clf, X_train, y_train_5, cv=3, scoring="accuracy")

from sklearn.model_selection import cross_val_predict
from sklearn.metrics import confusion_matrix

y_train_pred = cross_val_predict(sgd_clf, X_train, y_train_5, cv=3)
# Get predictions for every instance via cross-validation

cm = confusion_matrix(y_train_5, y_train_pred)
print(cm)
# Prints in the form [[TN, FP], [FN, TP]]

from sklearn.metrics import precision_score, recall_score, f1_score
precision_score(y_train_5, y_train_pred)  # precision
recall_score(y_train_5, y_train_pred)     # recall
f1_score(y_train_5, y_train_pred)         # F1 score (harmonic mean of precision and recall)
```

**Precision/Recall Curve & ROC Curve**

```python
from sklearn.metrics import precision_recall_curve, roc_curve

y_scores = cross_val_predict(sgd_clf, X_train, y_train_5, cv=3, method="decision_function")
# Instead of yes/no, get a confidence score (used to adjust the decision threshold)

precisions, recalls, thresholds = precision_recall_curve(y_train_5, y_scores)
fpr, tpr, thresholds = roc_curve(y_train_5, y_scores)
# These values can be plotted with matplotlib to compare visually
```

## 4. Multiclass Classification

Now we classify all ten digits (0–9), not just "5 or not."

```python
from sklearn.svm import SVC

svm_clf = SVC(random_state=42)
svm_clf.fit(X_train[:2000], y_train[:2000])
# scikit-learn automatically uses One-vs-One under the hood for SVM

svm_clf.predict([X_train[0]])
```

```python
from sklearn.multiclass import OneVsRestClassifier

ovr_clf = OneVsRestClassifier(SVC(random_state=42))
ovr_clf.fit(X_train[:2000], y_train[:2000])
# Explicitly wrap with OvR (One-vs-Rest) if you want that strategy instead
```

## 5. Error Analysis

We visualize the confusion matrix as a heatmap to see which digits the model confuses most often.

```python
from sklearn.metrics import ConfusionMatrixDisplay

y_train_pred = cross_val_predict(sgd_clf, X_train, y_train, cv=3)
ConfusionMatrixDisplay.from_predictions(y_train, y_train_pred, normalize="true")
# normalize="true": shows percentages per row, e.g. "of all actual 3s, what % got predicted as 5"
```

## 6. Multilabel Classification

A case where one instance can have multiple correct labels at once — e.g., "is it ≥7?" AND "is it odd?" answered simultaneously.

```python
import numpy as np
from sklearn.neighbors import KNeighborsClassifier

y_train_large = (y_train.astype('int8') >= 7)   # is it >= 7?
y_train_odd = (y_train.astype('int8') % 2 == 1) # is it odd?
y_multilabel = np.c_[y_train_large, y_train_odd]
# combine both True/False labels into one vector

knn_clf = KNeighborsClassifier()
knn_clf.fit(X_train, y_multilabel)
knn_clf.predict([X_train[0]])
# output like [False, True] -> "less than 7, and odd"
```

## 7. Multioutput Classification

An extension of multilabel where each label can take multiple values (like 0–255). The book's example: input a noisy image, output a cleaned-up version.

```python
noise = np.random.randint(0, 100, (len(X_train), 784))
X_train_mod = X_train + noise
# Add random noise to the original image to create a "dirty" input

y_train_mod = X_train
# the target is the original clean image itself

knn_clf.fit(X_train_mod, y_train_mod)
clean_digit = knn_clf.predict([X_train_mod[0]])
# Feed a noisy image in, get back a predicted clean image (784 pixel values)
```

## Quiz / New Learning

Q: In a dataset where 90% of samples are "normal" and 10% are "anomaly", why is accuracy alone misleading? What should you look at instead?
A: When 90% of the data is "normal", a model that always predicts "normal" gets 90% accuracy without learning anything useful — it's called the accuracy paradox. Instead, look at the confusion matrix, along with precision (of all predicted anomalies, how many were correct) and recall (of all actual anomalies, how many were caught). Often the F1 score (harmonic mean of the two) is used to summarize both in one number, especially with imbalanced data like this.

## Reference
- Official code examples: https://github.com/ageron/handson-ml3
