# Chapter 4: Training Models
Hands-On Machine Learning | Date: 2026-09-14 | Author: Yedam Kang

## 1. Linear Regression

Linear regression fits a straight line (or hyperplane) to the data: `y = θ₀ + θ₁x₁ + θ₂x₂ + ...`. The **Normal Equation** computes the best θ directly in one shot using calculus, without needing multiple iterations.

```python
import numpy as np
from sklearn.linear_model import LinearRegression

X = 2 * np.random.rand(100, 1)
y = 4 + 3 * X + np.random.randn(100, 1)
# Generate fake linear data with some random noise

lin_reg = LinearRegression()
lin_reg.fit(X, y)

lin_reg.intercept_, lin_reg.coef_
# intercept_: θ₀ (where the line crosses the y-axis)
# coef_: θ₁ (the slope of the line)
```

## 2. Gradient Descent

Gradient Descent finds the best parameters by taking small steps downhill on the loss function, like walking down a foggy mountain toward the lowest point. The **learning rate** controls step size — too big and it overshoots (diverges), too small and it's painfully slow.

```python
from sklearn.linear_model import SGDRegressor

sgd_reg = SGDRegressor(max_iter=1000, tol=1e-3, penalty=None, eta0=0.01)
# eta0: the learning rate
# max_iter: how many passes over the data at most
# penalty=None: no regularization for now (plain gradient descent)

sgd_reg.fit(X, y.ravel())
sgd_reg.intercept_, sgd_reg.coef_
```

There are three variants:
- **Batch Gradient Descent**: uses the whole dataset for every step (accurate but slow on big data)
- **Stochastic Gradient Descent (SGD)**: uses one random instance per step (fast but noisy/unstable)
- **Mini-batch Gradient Descent**: uses a small random subset per step (a practical middle ground)

## 3. Polynomial Regression

When data isn't a straight line, we add squared/cubed terms (x², x³...) as new features and then fit a linear model to those — effectively fitting a curve.

```python
from sklearn.preprocessing import PolynomialFeatures

poly_features = PolynomialFeatures(degree=2, include_bias=False)
X_poly = poly_features.fit_transform(X)
# Adds x^2 as a new feature alongside the original x

lin_reg = LinearRegression()
lin_reg.fit(X_poly, y)
# Now fitting a curve, using the same linear regression tool
```

⚠️ Warning: increasing the degree too much overfits the training data — the curve wiggles to match noise instead of the true pattern, and fails on new data.

## 4. Learning Curves

Learning curves plot error against training set size to diagnose **underfitting** (both training and validation error stay high) vs **overfitting** (training error is low but validation error is high).

```python
from sklearn.model_selection import learning_curve

train_sizes, train_scores, valid_scores = learning_curve(
    LinearRegression(), X, y, train_sizes=np.linspace(0.01, 1.0, 40), cv=5,
    scoring="neg_root_mean_squared_error")
# Trains the model on increasingly larger subsets of data, cross-validating each time
```

This connects to the **bias-variance tradeoff**: a model that's too simple has high *bias* (systematically wrong), a model that's too complex has high *variance* (wildly sensitive to the specific training data). The goal is to find the balance between the two.

## 5. Regularized Linear Models

Regularization shrinks the model's weights so it doesn't overfit.

```python
from sklearn.linear_model import Ridge, Lasso, ElasticNet

ridge_reg = Ridge(alpha=1, solver="cholesky")
# Ridge (L2): penalizes the sum of squared weights -> shrinks weights toward zero

lasso_reg = Lasso(alpha=0.1)
# Lasso (L1): penalizes the sum of absolute weights -> can push some weights to EXACTLY zero
# (this acts like automatic feature selection)

elastic_net = ElasticNet(alpha=0.1, l1_ratio=0.5)
# ElasticNet: a mix of Ridge and Lasso, controlled by l1_ratio
```

**Early Stopping** is another regularization trick: stop training as soon as validation error starts increasing again, instead of letting it keep training (and overfitting).

## 6. Logistic Regression

Despite the name "regression," this is actually used for **classification**. It passes the linear regression output through a **sigmoid function** to squash it into a probability between 0 and 1.

```python
from sklearn.linear_model import LogisticRegression

log_reg = LogisticRegression()
log_reg.fit(X_train, y_train_5)
# Predicts the probability that an instance belongs to the positive class (e.g., "is a 5")

log_reg.predict_proba([X_train[0]])
# Returns something like [0.2, 0.8] -> 80% chance it IS a 5
```

**Softmax Regression** extends this to multiple classes at once, outputting a probability for each class that all sum to 1.

```python
softmax_reg = LogisticRegression(multi_class="multinomial")
softmax_reg.fit(X_train, y_train)
# Directly predicts one of several classes (e.g., digits 0-9), not just yes/no
```

## Quiz / New Learning

Q: Why is Logistic Regression called a "regression" even though it's used for classification?

A: Because internally it computes a continuous numeric value (a weighted sum of the inputs, just like linear regression), and only at the very last step does it convert that number into a class decision using the sigmoid function and a probability threshold. The underlying math is regression; the output usage is classification.

## Reference
- Official code examples: https://github.com/ageron/handson-ml3
