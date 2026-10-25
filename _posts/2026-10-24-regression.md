---
title:  "Linear and Logistic Regression"
categories: [Math,AI]
tags: [Regression]
math: true
image: /assets/img/2026-10-24/regression.jpg
---


## Introduction

Welcome! This blog post summarizes the core concepts of **Linear and Logistic Regression** for machine learning, inspired by [Andrew Ng's](https://de.wikipedia.org/wiki/Andrew_Ng) renowned online course.

All code examples are written in **Python using NumPy**. If you need to set up your environment, you can install NumPy quickly via terminal:

```bash
pip install numpy

```


## Notation and Data Structure

To formalize the problem, we define our dataset and variables as follows:

* **Training Set ($X$):** An $m \times n$ matrix containing $m$ training examples:

$$X = \{x^{(1)}, x^{(2)}, \dots, x^{(m)}\}$$



where each example $x^{(i)}$ consists of features $(x^{(i)}_0, x^{(i)}_1, \dots, x^{(i)}_n) \in \mathbb{R}$.
* **Target Vector ($Y$):** An $m \times 1$ column vector containing the target associated with each example:

$$Y = \begin{bmatrix} y^{(1)} \\ y^{(2)} \\ \vdots \\ y^{(m)} \end{bmatrix}$$



### Target Types by Regression Task

* **Linear Regression:** Continuous numeric values where $y^{(i)} \in \mathbb{R}$.
* **Logistic Regression:** Discrete classes mapped to integer labels such as $0, 1, \dots, \vert{}C\vert{}$.


## Hypothesis Function

The goal of learning is to produce a **hypothesis function** $h_{\theta}: \mathbb{R}^{n+1} \rightarrow \mathbb{R}$ parameterized by $\theta$ that predicts target values for unseen data. To enable efficient vectorization, we introduce an intercept feature $x_0^{(i)} = 1$ for all examples $i \in \{1, \dots, m\}$.

### 1. Linear Regression

The vectorized hypothesis for a single example and the full dataset matrix is:

$$h_{\theta}(x^{(i)}) = \theta^T x^{(i)}$$

$$H_{\theta}(X) = X\theta$$

**Python (NumPy) Implementation:**

```python
import numpy as np

# Add intercept column x_0 = 1
X = np.hstack([np.ones((X.shape[0], 1)), X])

# Linear regression hypothesis: (m x (n+1)) @ ((n+1) x 1) = m x 1
h_lin = X @ theta

```

### 2. Logistic Regression

Logistic regression outputs an estimated probability $P(y=1 \mid x^{(i)}; \theta)$. We pass $X\theta$ through the [Sigmoid Function](https://en.wikipedia.org/wiki/Sigmoid_function) to constrain outputs between $0$ and $1$:

$$g(z) = \frac{1}{1 + e^{-z}} \implies h_{\theta}(x) = \frac{1}{1 + e^{-\theta^T x}}$$

**Python (NumPy) Implementation:**

```python
# Vectorized Sigmoid Hypothesis
h_log = 1 / (1 + np.exp(-X @ theta))

```


## Cost Function

The cost function $J(\theta)$ measures the error between predictions and actual targets. The learning objective is to find parameters $\theta$ that minimize $J(\theta)$.

### 1. Linear Regression (Mean Squared Error)

Uses the [Mean Squared Error (MSE)](https://en.wikipedia.org/wiki/Mean_squared_error) loss:

$$J(\theta) = \frac{1}{2m} \sum_{i=1}^{m} \left( h_{\theta}(x^{(i)}) - y^{(i)} \right)^2$$

**Python (NumPy) Implementation:**

```python
error = (h_lin - y) ** 2  # Element-wise squared errors
J = np.sum(error) / (2 * m)  # Average squared loss

```

### 2. Logistic Regression (Log Loss / Cross-Entropy)

Penalizes incorrect confident predictions using log loss:

$$J(\theta) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y^{(i)} \log(h_{\theta}(x^{(i)})) + (1 - y^{(i)}) \log(1 - h_{\theta}(x^{(i)})) \right]$$

**Python (NumPy) Implementation:**

```python
# Clip predictions to prevent log(0) errors
eps = 1e-15
h_log = np.clip(h_log, eps, 1 - eps)

error = y * np.log(h_log) + (1 - y) * np.log(1 - h_log)
J = -np.sum(error) / m

```


## Gradient Descent

[Gradient Descent](https://en.wikipedia.org/wiki/Gradient_descent) is an iterative optimization algorithm that updates parameters in the direction of the negative gradient $-\nabla J(\theta)$ to find the minimum.

### Update Rule for Linear Regression

$$\theta_j = \theta_j - \alpha \frac{1}{m} \sum_{i=1}^m \left( h_{\theta}(x^{(i)}) - y^{(i)} \right) x_j^{(i)}$$

**Python (NumPy) Implementation:**

```python
m, n = X.shape
X = np.hstack([np.ones((m, 1)), X])  # Add x_0 = 1 column
theta = np.zeros((n + 1, 1))         # Initialize parameters
iterations = 1000
alpha = 0.001                        # Learning rate

for _ in range(iterations):
    h = X @ theta                    # Linear regression hypothesis
    # h = 1 / (1 + np.exp(-X @ theta)) # Uncomment for logistic regression
    
    loss = h - y
    gradient = (X.T @ loss) / m
    theta -= alpha * gradient        # Update parameters

```

### Learning Rate & Feature Scaling

* **Learning Rate ($\alpha$):** Must be tuned carefully. If too small, convergence is slow; if too large, $J(\theta)$ may diverge. Typical values range from $0.001$ to $0.1$.
* **Feature Scaling:** Speeds up convergence by scaling features to comparable ranges.
* **Min-Max Scaling:** $x_j^{(i)} = \frac{x_j^{(i)} - \min(x_j)}{\max(x_j) - \min(x_j)}$
* **Mean Normalization:** $x_j^{(i)} = \frac{x_j^{(i)} - \text{mean}(x_j)}{\max(x_j) - \min(x_j)}$



## Overfitting and Regularization

**Overfitting** occurs when a model fits training data too closely ($\approx 0$ training error) but fails to generalize. **Regularization** adds a penalty term controlled by $\lambda$ to constrain large parameter values. Setting $\lambda$ too high can cause **underfitting**.

### 1. Regularized Linear Regression

**Cost Function:**


$$J(\theta) = \frac{1}{2m} \sum_{i=1}^m \left( h_{\theta}(x^{(i)}) - y^{(i)} \right)^2 + \frac{\lambda}{2m} \sum_{j=1}^n \theta_j^2$$

**Update Rule:**


$$\theta_j = \theta_j \left(1 - \alpha \frac{\lambda}{m}\right) - \alpha \frac{1}{m} \sum_{i=1}^m \left( h_{\theta}(x^{(i)}) - y^{(i)} \right) x_j^{(i)}$$

### 2. Regularized Logistic Regression

**Cost Function:**


$$J(\theta) = -\frac{1}{m} \sum_{i=1}^m \left[ y^{(i)} \log(h_{\theta}(x^{(i)})) + (1 - y^{(i)}) \log(1 - h_{\theta}(x^{(i)})) \right] + \frac{\lambda}{2m} \sum_{j=1}^n \theta_j^2$$

**Update Rule:**


$$\theta_j = \begin{cases} \theta_j - \alpha \frac{1}{m} \sum_{i=1}^m \left( h_{\theta}(x^{(i)}) - y^{(i)} \right) x_j^{(i)} & \text{for } j = 0 \\  \theta_j - \alpha \left[ \frac{1}{m} \sum_{i=1}^m \left( h_{\theta}(x^{(i)}) - y^{(i)} \right) x_j^{(i)} + \frac{\lambda}{m}\theta_j \right] & \text{for } j > 0 \end{cases}$$


Here is an additional section you can append to your blog post. It provides a complete, runnable example using **scikit-learn** to generate synthetic data, tracks the cost at each step of gradient descent, and uses **matplotlib** to visualize convergence.


## Practical Example: End-to-End Implementation

To see how everything ties together, here is a complete Python script for **Linear Regression with Gradient Descent**. This example generates synthetic data, normalizes the features, runs optimization while tracking the cost history, and plots the convergence curve.

### Python Implementation

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import make_regression

# 1. Generate synthetic dataset
X, y = make_regression(n_samples=500, n_features=1, noise=15, random_state=42)
y = y.reshape(-1, 1)  # Reshape to column vector

# 2. Feature scaling (Mean Normalization)
X = (X - np.mean(X, axis=0)) / np.std(X, axis=0)

# 3. Add intercept column (x_0 = 1) and initialize parameters
m = X.shape[0]
X = np.hstack([np.ones((m, 1)), X])
theta = np.zeros((X.shape[1], 1))

# 4. Hyperparameters
iterations = 300
alpha = 0.05
cost_history = []

# 5. Gradient Descent Optimization Loop
for i in range(iterations):
    h = X @ theta                  # Hypothesis
    loss = h - y                   # Error vector
    gradient = (X.T @ loss) / m    # Gradient calculation
    theta -= alpha * gradient      # Parameter update
    
    # Compute and save cost J(theta)
    cost = np.sum(loss ** 2) / (2 * m)
    cost_history.append(cost)

print(f"Optimized Parameters (theta): {theta.ravel()}")

# 6. Plotting Cost History
plt.figure(figsize=(8, 4))
plt.plot(range(iterations), cost_history, color='b', linewidth=2)
plt.xlabel("Iterations")
plt.ylabel("Cost J(theta)")
plt.title("Gradient Descent Convergence")
plt.grid(True, linestyle="--", alpha=0.6)
plt.show()

```

### Why This Matters

* **Monitoring Convergence:** Plotting the cost history lets you visually verify that $J(\theta)$ decreases with every iteration. If the curve oscillates or shoots upward, your learning rate ($\alpha$) is too high.
* **Vectorization Benefits:** Using matrix operations (`X @ theta` and `X.T @ loss`) instead of explicit `for` loops speeds up execution significantly on larger datasets.



## Additional Resources

* **External Video:** [Gradient Descent in 3 Minutes](https://www.youtube.com/watch?v=qg4PchTECck)


