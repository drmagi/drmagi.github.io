---
title: Linear Algebra Essentials
description: An introduction to essential linear algebra fundamentals with practical Python NumPy code examples. Created with AI support. 
categories: [Math]
tags: [Math]
math: true
---


# Linear Algebra Essentials: From Vectors to Tensors

Linear algebra is the mathematical foundation of data science, machine learning, and computer graphics. Understanding how data is structured and manipulated in multi-dimensional spaces is essential for writing efficient code.

Let's break down the core building blocks: **Vectors**, **Matrices**, and **Tensors**, along with their fundamental operations.



## 1. Vectors

A **vector** is a one-dimensional array of numbers. Depending on the context:

* In **physics and geometry**, a vector represents a quantity with both magnitude and direction (e.g., velocity, force).
* In **computer science and machine learning**, a vector represents a list of features or attributes for a single data point (e.g., age, income, height).

Vectors can be written as **row vectors** (e.g., $\left[ 1, 3, 5 \right]$) or **column vectors** (e.g., $\left[ \begin{array}{c} 1 \\ 3 \\ 5 \end{array} \right] \in \mathbb{R}^3$).

### NumPy Example: Creating Vectors

```python
import numpy as np

# A row vector (1D array)
v_row = np.array([1, 3, 5])
print("Row Vector:", v_row)
print("Shape:", v_row.shape)

```



## 2. Matrices

A **matrix** is a two-dimensional array of numbers arranged in rows and columns.

* **Notation:** Matrices are traditionally sized as $\text{rows} \times \text{columns}$ ($m \times n$).
* **Example:** A matrix with 2 rows and 3 columns has a shape of $2 \times 3$:

$$\begin{bmatrix} 3 & 4 & 5 \\ 3 & 0 & 0 \end{bmatrix}$$



### NumPy Example: Creating and Inspecting Matrices

```python
# A 2x3 matrix
matrix = np.array([[3, 4, 5], 
                   [3, 0, 0]])
print("Matrix:\n", matrix)
print("Shape (Rows, Columns):", matrix.shape)

```



## 3. Tensors

A **tensor** is a generalization of vectors and matrices to an arbitrary number of dimensions ($n$-dimensional array).

* A 0-dimensional tensor is a **scalar** (a single number).
* A 1-dimensional tensor is a **vector**.
* A 2-dimensional tensor is a **matrix**.
* A 3-dimensional tensor can represent things like an RGB image (Height $\times$ Width $\times$ Color Channels).

### NumPy Example: Creating Tensors

```python
# A 3-dimensional tensor of zeros with shape (2, 3, 4)
tensor_3d = np.zeros((2, 3, 4))
print("Tensor Shape:", tensor_3d.shape)
print("Tensor Dimensions (ndim):", tensor_3d.ndim)

```



## 4. Fundamental Operations

### A. Matrix Addition and Subtraction

To add or subtract two matrices, they must have the **exact same dimensions**. The operation is performed element-wise (adding/subtracting the corresponding entries at row $i$, column $j$).

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# Element-wise addition
print("Addition:\n", A + B)

# Element-wise subtraction
print("Subtraction:\n", B - A)

```



### B. Dot Product

The dot product takes two vectors of the same length and returns a single scalar value. It is calculated by multiplying corresponding elements and summing up the results:


$$\mathbf{a} \cdot \mathbf{b} = a_1b_1 + a_2b_2 + \dots + a_nb_n$$

```python
v1 = np.array([2, 3])
v2 = np.array([4, 5])

# Using numpy dot function or the @ operator for 1D arrays
dot_product = np.dot(v1, v2)
print("Dot Product:", dot_product)  # Output: 2*4 + 3*5 = 23

```



### C. Matrix Multiplication

Unlike addition, matrix multiplication does not require matrices to have the same shape. To multiply matrix $A$ of shape $(n, m)$ by matrix $B$ of shape $(m, l)$, **the number of columns of $A$ must equal the number of rows of $B$**. The resulting matrix will have the shape $(n, l)$.

```python
# A is (2, 3)
A = np.array([[3, 4, 5], 
              [3, 0, 0]])

# B is (3, 2)
B = np.array([[1, 2], 
              [3, 4], 
              [5, 6]])

# Matrix multiplication using '@' operator (or np.matmul)
result = A @ B
print("Matrix Multiplication Result (2x2):\n", result)
print("Result Shape:", result.shape)

```



### D. Transpose

The transpose of a matrix flips it across its main diagonal, turning rows into columns and columns into rows. If matrix $A$ has shape $(m, n)$, its transpose $A^T$ has shape $(n, m)$.

*An important property:* $(AB)^T = B^T A^T$

```python
arr = np.array([[1, -2, 1], 
                [2, -4, 5]])

# Transposing using .T
transposed_arr = arr.T
print("Transposed Array:\n", transposed_arr)

```



### E. Vector Norm (Magnitude)

In machine learning and optimization, we often need to measure how "large" a vector is—for instance, to calculate error distances (Loss functions) or regularize models to prevent overfitting.

The **Vector Norm** (specifically the Euclidean or L2 norm) measures the length of a vector from the origin to its coordinate point. For a vector $\mathbf{v} = [v_1, v_2, \dots, v_n]$, the L2 norm is calculated as:


$$\Vert{}\mathbf{v}\Vert{}_2 = \sqrt{v_1^2 + v_2^2 + \dots + v_n^2}$$

### NumPy Example: Calculating Vector Norms

```python
v = np.array([3, 4])

# Calculate the Euclidean (L2) norm
norm = np.linalg.norm(v)
print("Vector:", v)
print("L2 Norm (Magnitude):", norm)  # Output: sqrt(3^2 + 4^2) = 5.0

```

## Summary and Conclusion

Linear algebra is the computational language that powers modern technology. From training massive deep learning models and processing high-resolution images to running physics simulations in video games, multi-dimensional data structures are everywhere.