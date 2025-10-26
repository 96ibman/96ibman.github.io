---
layout: post
title: "Understanding Eigenvalues and Eigenvectors"
date: 2021-08-15
---

Eigenvalues and eigenvectors appear everywhere in mathematics, data analysis, and machine learning, from PCA to stability analysis and linear transformations.  
But the idea itself is very intuitive.

## Step 1: What Are Eigenvalues and Eigenvectors?

Suppose you have a square matrix $A$.  
An **eigenvector** of $A$ is a non-zero vector $x$ such that when you multiply $A$ by $x$, the result is just a **scaled version** of $x$:

$$
A x = \lambda x
$$

Here $\lambda$ is a real number called the **eigenvalue** corresponding to that eigenvector.

So, multiplying $A$ by $x$ does not change the **direction** of $x$; it only changes its **length** (or possibly flips its direction if $\lambda$ is negative).

## Step 2: Example Matrix

Let us work through a simple example:

$$
A =
\begin{bmatrix}
0 & 1 \\
-2 & -3
\end{bmatrix}
$$

Our goal is to find its eigenvalues and eigenvectors.

## Step 3: Setting Up the Equation

We start with

$$
A x = \lambda x
$$

To make this easier to work with, multiply $x$ by the **identity matrix** $I$, which does not change anything:

$$
A x = I \lambda x
$$

Rearrange all terms to one side:

$$
A x - I \lambda x = 0
$$

Factor out $x$:

$$
(A - \lambda I)x = 0
$$

This equation means that for some non-zero vector $x$, the matrix $(A - \lambda I)$ makes the result zero.

That can only happen if $(A - \lambda I)$ is **not invertible**, which implies that its determinant is zero:

$$
\det(A - \lambda I) = 0
$$

This is called the **characteristic equation**.

## Step 4: Compute the Determinant

Compute $A - \lambda I$:

$$
A - \lambda I =
\begin{bmatrix}
0 - \lambda & 1 \\
-2 & -3 - \lambda
\end{bmatrix}
=
\begin{bmatrix}
-\lambda & 1 \\
-2 & -3 - \lambda
\end{bmatrix}
$$

Now find its determinant:

$$
\det(A - \lambda I) = (-\lambda)(-3 - \lambda) - (1)(-2)
$$

Simplify:

$$
\det(A - \lambda I) = \lambda(3 + \lambda) + 2
$$

$$
= \lambda^2 + 3\lambda + 2
$$

Set it equal to zero:

$$
\lambda^2 + 3\lambda + 2 = 0
$$

## Step 5: Solve for the Eigenvalues

Factor the quadratic:

$$
(\lambda + 1)(\lambda + 2) = 0
$$

So the eigenvalues are

$$
\lambda_1 = -1, \quad \lambda_2 = -2
$$

## Step 6: Find the Eigenvector for $\lambda = -1$

Substitute $\lambda = -1$ into $(A - \lambda I)x = 0$:

$$
(A + I)x = 0
$$

Compute $A + I$:

$$
A + I =
\begin{bmatrix}
0 & 1 \\
-2 & -3
\end{bmatrix}
+
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
=
\begin{bmatrix}
1 & 1 \\
-2 & -2
\end{bmatrix}
$$

Now we solve

$$
\begin{bmatrix}
1 & 1 \\
-2 & -2
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2
\end{bmatrix}
= 0
$$

From the first row:

$$
x_1 + x_2 = 0
$$

So

$$
x_2 = -x_1
$$

We can choose any non-zero value for $x_1$.  
A simple choice is $x_1 = 1$, which gives $x_2 = -1$.

Thus, one eigenvector corresponding to $\lambda = -1$ is

$$
x =
\begin{bmatrix}
1 \\
-1
\end{bmatrix}
$$

## Step 7: Verify

Let us check that it works:

$$
A x =
\begin{bmatrix}
0 & 1 \\
-2 & -3
\end{bmatrix}
\begin{bmatrix}
1 \\
-1
\end{bmatrix}
=
\begin{bmatrix}
-1 \\
1
\end{bmatrix}
= (-1)
\begin{bmatrix}
1 \\
-1
\end{bmatrix}
$$

It matches $A x = \lambda x$ for $\lambda = -1$.  
So this is indeed a valid eigenvector.

## Step 8: Find the Eigenvector for $\lambda = -2$

Substitute $\lambda = -2$ into $(A - \lambda I)x = 0$:

$$
(A + 2I)x = 0
$$

Compute $A + 2I$:

$$
A + 2I =
\begin{bmatrix}
0 & 1 \\
-2 & -3
\end{bmatrix}
+
\begin{bmatrix}
2 & 0 \\
0 & 2
\end{bmatrix}
=
\begin{bmatrix}
2 & 1 \\
-2 & -1
\end{bmatrix}
$$

Now solve:

$$
\begin{bmatrix}
2 & 1 \\
-2 & -1
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2
\end{bmatrix}
= 0
$$

From the first row:

$$
2x_1 + x_2 = 0
$$

So

$$
x_2 = -2x_1
$$

Choose $x_1 = 1$, then $x_2 = -2$.

The eigenvector corresponding to $\lambda = -2$ is

$$
x =
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
$$

## Step 9: Verify

$$
A x =
\begin{bmatrix}
0 & 1 \\
-2 & -3
\end{bmatrix}
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
=
\begin{bmatrix}
-2 \\
4
\end{bmatrix}
= (-2)
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
$$

Again, it satisfies $A x = \lambda x$ for $\lambda = -2$.

## Step 10: Summary

For the matrix

$$
A =
\begin{bmatrix}
0 & 1 \\
-2 & -3
\end{bmatrix}
$$

we found

| Eigenvalue ($\lambda$) | Eigenvector ($x$) |
|:-----------------------:|:----------------:|
| $-1$ | $\begin{bmatrix} 1 \\ -1 \end{bmatrix}$ |
| $-2$ | $\begin{bmatrix} 1 \\ -2 \end{bmatrix}$ |

## Step 11: Intuition

Each eigenvector defines a direction in which the matrix $A$ acts as simple scaling.  
Instead of rotating or distorting the vector, $A$ just stretches or shrinks it by its eigenvalue.

That is why eigenvalues and eigenvectors are so fundamental. They reveal the **intrinsic directions** and **scaling factors** of a linear transformation.

## Step 12: Verify in Python

```python
import numpy as np

A = np.array([[0, 1],
              [-2, -3]])

values, vectors = np.linalg.eig(A)
print("Eigenvalues:", values)
print("Eigenvectors:\n", vectors)
```
```
Eigenvalues: [-1. -2.]
Eigenvectors:
 [[ 0.70710678  0.4472136 ]
 [-0.70710678 -0.89442719]]
```

---

## Note on Verification

If you compare the Python output with our manually computed eigenvectors, they might look different at first glance. 

However, they actually represent the **same directions**.  
The difference is only in **scaling**.

Eigenvectors are not unique in magnitude.  
If $x$ is an eigenvector, then any non-zero multiple $c x$ (for example $2x$ or $-x$) is also an eigenvector for the same eigenvalue.

NumPy’s `np.linalg.eig` automatically **normalizes** eigenvectors to have length one.  
Let us verify this.

For $\lambda = -1$ we found

$$
x =
\begin{bmatrix}
1 \\
-1
\end{bmatrix}
$$

Normalizing it:

$$
\frac{1}{\sqrt{1^2 + (-1)^2}}
\begin{bmatrix}
1 \\
-1
\end{bmatrix}
=
\begin{bmatrix}
0.7071 \\
-0.7071
\end{bmatrix}
$$

which matches the **first** column of NumPy’s result.

For $\lambda = -2$ we found

$$
x =
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
$$

Normalizing it:

$$
\frac{1}{\sqrt{1^2 + (-2)^2}}
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
=
\begin{bmatrix}
0.4472 \\
-0.8944
\end{bmatrix}
$$

which matches the **second** column of NumPy’s result.

So both computations are consistent.  
NumPy simply returns **unit-length eigenvectors**, while we worked with the raw, unnormalized versions.



## Conclusion
An eigenvector of a matrix is a direction that the matrix does not rotate, only stretches or compresses.
The eigenvalue tells you how much stretching or compression occurs along that direction.

Understanding eigenvalues and eigenvectors is essential for working with dimensionality reduction, PCA, linear dynamical systems, and many areas of machine learning.


