---
layout: post
title: "Understanding Variance and Covariance"
date: 2021-08-01
---

Variance and covariance are two sides of the same idea.  
Variance tells us how much a single variable fluctuates.  
Covariance tells us how two variables fluctuate together.

We start with variance, then extend it naturally to covariance.

---

## Step 1: Variance

Before defining variance, let’s recall what the **expected value** means.

The expected value $\mathbb{E}(x)$ is simply the **average** or **mean** of a random variable $x$.  
It represents the central or typical value that $x$ tends to take.

For a sample of $n$ data points $x_1, x_2, \dots, x_n$, we compute it as

$$
\mathbb{E}(x) = \frac{1}{n}\sum_{i=1}^{n} x_i
$$

Now, **variance** measures how far the data points are spread out around this mean.

Formally, it is the expected value of the squared deviation from the mean:

$$
\mathrm{var}(x) = \mathbb{E}\big[(x - \mathbb{E}(x))^2\big]
$$

Let’s unpack that.

- The inner $\mathbb{E}(x)$ is just the **mean** of $x$.  
- The expression $(x - \mathbb{E}(x))$ measures how far each value is from that mean.  
- Squaring it makes all deviations positive and emphasizes larger gaps.  
- The outer $\mathbb{E}$ means we **average those squared deviations**.

So the variance is literally the **average squared distance from the mean**.

Consider this simple dataset of two features $F_1$ and $F_2$:

|        | $F_1$ | $F_2$ |
|:-------|:------:|:------:|
| Data 1 | 1 | 1 |
| Data 2 | 3 | 0 |
| Data 3 | -1 | -1 |

The sample means are

|        | $F_1$ | $F_2$ |
|:-------|:------:|:------:|
| **Mean** | **1** | **0** |

Now compute the deviations and squared deviations:

| Data | $F_1$ | $F_1 - \mathbb{E}(F_1)$ | $(F_1 - \mathbb{E}(F_1))^2$ |
|:----|:--:|:--:|:--:|
| 1 | 1 | 0 | 0 |
| 2 | 3 | 2 | 4 |
| 3 | -1 | -2 | 4 |

$$
\mathrm{var}(F_1) = \frac{0 + 4 + 4}{3} = \frac{8}{3}
$$

Similarly for $F_2$:

| Data | $F_2$ | $F_2 - \mathbb{E}(F_2)$ | $(F_2 - \mathbb{E}(F_2))^2$ |
|:----|:--:|:--:|:--:|
| 1 | 1 | 1 | 1 |
| 2 | 0 | 0 | 0 |
| 3 | -1 | -1 | 1 |

$$
\mathrm{var}(F_2) = \frac{1 + 0 + 1}{3} = \frac{2}{3}
$$

---

## Step 2: From Variance to Covariance

Variance looks at how one variable deviates from its mean.  
Covariance extends that idea to measure how **two variables** vary together.

The definition of covariance between two random variables $A$ and $B$ is

$$
\mathrm{cov}(A, B) = \mathbb{E}\big[(A - \mathbb{E}(A))(B - \mathbb{E}(B))\big]
$$

We can show that this is equivalent to

$$
\mathrm{cov}(A, B) = \mathbb{E}(AB) - \mathbb{E}(A)\mathbb{E}(B)
$$

Let’s expand it step by step.

Start from the definition:

$$
\mathrm{cov}(A, B) = \mathbb{E}\big[(A - \mathbb{E}(A))(B - \mathbb{E}(B))\big]
$$

Expand the product inside the expectation:

$$
(A - \mathbb{E}(A))(B - \mathbb{E}(B))
= AB - A\mathbb{E}(B) - B\mathbb{E}(A) + \mathbb{E}(A)\mathbb{E}(B)
$$

Now take the expectation $\mathbb{E}$ of both sides.  
Since expectation is **linear**, we can distribute it across the terms:

$$
\mathbb{E}[AB - A\mathbb{E}(B) - B\mathbb{E}(A) + \mathbb{E}(A)\mathbb{E}(B)]
= \mathbb{E}(AB) - \mathbb{E}[A\mathbb{E}(B)] - \mathbb{E}[B\mathbb{E}(A)] + \mathbb{E}[\mathbb{E}(A)\mathbb{E}(B)]
$$

Note that $\mathbb{E}(A)$ and $\mathbb{E}(B)$ are just **constants** (numbers), not random variables.  
So we can pull them out of the expectation:

$$
\mathbb{E}[A\mathbb{E}(B)] = \mathbb{E}(B)\mathbb{E}(A)
$$

$$
\mathbb{E}[B\mathbb{E}(A)] = \mathbb{E}(A)\mathbb{E}(B)
$$

$$
\mathbb{E}[\mathbb{E}(A)\mathbb{E}(B)] = \mathbb{E}(A)\mathbb{E}(B)
$$

Substitute these back in:

$$
\mathrm{cov}(A,B) = \mathbb{E}(AB) - \mathbb{E}(A)\mathbb{E}(B) - \mathbb{E}(A)\mathbb{E}(B) + \mathbb{E}(A)\mathbb{E}(B)
$$

Simplify:

$$
\mathrm{cov}(A,B) = \mathbb{E}(AB) - \mathbb{E}(A)\mathbb{E}(B)
$$

Therefore,

$$
\mathrm{cov}(A, B) = \mathbb{E}(AB) - \mathbb{E}(A)\mathbb{E}(B)
$$

In words: covariance is the **expected value of the product of the two variables** minus the **product of their expected values**.  
This form is often more convenient for direct computation from data.

When both variables increase and decrease together, covariance is **positive**.  
When one increases while the other decreases, covariance is **negative**.  
If they are unrelated, covariance is **zero**.

---

## Step 3: Computing Covariance

Add a column for the product $F_1F_2$:

|        | $F_1$ | $F_2$ | $F_1F_2$ |
|:-------|:------:|:------:|:------:|
| Data 1 | 1 | 1 | 1 |
| Data 2 | 3 | 0 | 0 |
| Data 3 | -1 | -1 | 1 |
| **Mean** | 1 | 0 | 2/3 |

Then

$$
\mathrm{cov}(F_1, F_2) = \mathbb{E}(F_1F_2) - \mathbb{E}(F_1)\mathbb{E}(F_2)
$$

$$
\mathrm{cov}(F_1, F_2) = \frac{2}{3} - 1 \cdot 0 = \frac{2}{3}
$$

---

## Step 4: Covariance with Itself

If we apply covariance to the same variable, we get variance again:

$$
\mathrm{cov}(A, A) = \mathrm{var}(A)
$$

We can verify this numerically:

|        | $F_1$ | $F_2$ | $F_1^2$ | $F_2^2$ |
|:-------|:------:|:------:|:------:|:------:|
| Data 1 | 1 | 1 | 1 | 1 |
| Data 2 | 3 | 0 | 9 | 0 |
| Data 3 | -1 | -1 | 1 | 1 |
| **Mean** | 1 | 0 | 11/3 | 2/3 |

So

$$
\mathrm{cov}(F_1, F_1) = \frac{11}{3} - 1^2 = \frac{8}{3}
$$

and

$$
\mathrm{cov}(F_2, F_2) = \frac{2}{3} - 0^2 = \frac{2}{3}
$$

---

## Step 5: The Covariance Matrix

Now we can write the covariance matrix:

|        | $F_1$ | $F_2$ |
|:-------|:------:|:------:|
| **$F_1$** | 8/3 | 2/3 |
| **$F_2$** | 2/3 | 2/3 |

The diagonal entries are variances, and the off-diagonal entries are covariances.  
This matrix is symmetric because $\mathrm{cov}(F_1, F_2) = \mathrm{cov}(F_2, F_1)$.

---

## Step 6: Verify in Python

```python
import numpy as np

F1 = [1, 3, -1]
F2 = [1, 0, -1]

data = np.array([F1, F2])

covMatrix = np.cov(data, bias=True)
print(covMatrix)
```
```
[[2.66666667 0.66666667]
 [0.66666667 0.66666667]]
```

## Step 7: A Note on Normalization

In our calculation, we divided by $n$.  
This is called **biased normalization** because it is biased toward the sample mean.

When we divide by $n$, the estimate has lower variance but remains biased.  
It does not converge to the true population covariance as $n$ grows.

Using $n - 1$ instead gives an **unbiased** estimator:

$$
\mathrm{cov}_{\text{unbiased}}(x, y) = \frac{1}{n - 1}\sum_i (x_i - \mathbb{E}(x))(y_i - \mathbb{E}(y))
$$

This is the version most statistical software packages use by default.

---

## Conclusion

Variance tells you how much a single variable spreads.  
Covariance tells you how two variables move together.  
The covariance matrix collects these relationships into one structure, describing the shape and direction of variation in your data.
