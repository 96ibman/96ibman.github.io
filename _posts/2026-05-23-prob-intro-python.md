--- 
layout: post
title: "Probabilities 101"
date: 2026-05-23
--- 

## Overview

In this post, we will learn about:

1. Sample Space
2. Events
3. Random Variables
4. Probability Functions
5. Conditional Probability
6. Independence

 

# 1. Sample Space

A sample space is the set of all possible outcomes.

Mathematically, it is usually written as $\Omega$ (pronounced as Omega)

 

## Example

Suppose we roll a fair six sided die.

The possible outcomes are:

$$
\Omega = \{1,2,3,4,5,6\}
$$

 

**In Python:**

```python
Omega = [1, 2, 3, 4, 5, 6]
```

This means:

- 1 is a possible outcome
- 2 is a possible outcome
- ...
- 6 is a possible outcome

 

# 2. Probability Function

A probability function tells us:

> How likely each outcome is.

Mathematically, for an outcome $\omega \in \Omega$, we define the probability of $\omega$:

$$
P(w)
$$

 

## Example

For a fair die:

$$
P(w) = \frac{1}{6}
$$

for every outcome.

 

**In Python:**

```python
def P(w):
    return 1 / 6
```

This means:

```python
P(1) = 1/6
P(2) = 1/6
P(3) = 1/6
...
```

 

# 3. Events

An event is simply:

> A collection of outcomes.

 

## Example

The event:

> Rolling an even number

contains these outcomes:

$$
\{2,4,6\}
$$

Another event:

> Rolling a number greater than 3

contains:

$$
\{4,5,6\}
$$

 

## Note

Events are subsets of the sample space.

Since:

$$
\Omega = \{1,2,3,4,5,6\}
$$

every event must contain outcomes from this set.

 

# 4. Random Variables

A random variable is simply a function from the sample space to the domain of the random variable:

$$
X : \Omega \rightarrow Values
$$

This means:

> The random variable takes an outcome from the sample space and maps it to some value.

In Python, we also represent random variables as python functions. It receives an outcome `w` and returns some property of that outcome.

 

## Example 1: Is the number even?

Suppose:

```python
w = 4
```

We define:

```python
def IsEven(w):
    return 'yes' if w % 2 == 0 else 'no'
```

Now:

```python
IsEven(4)
```

returns:

```python
'yes'
```

while:

```python
IsEven(5)
```

returns:

```python
'no'
```

So the random variable extracts information:

> Is this outcome even or not?

 

## Visual Interpretation

The random variable transforms outcomes.

| Outcome \(w\) | IsEven(w) |
|---|---|
| 1 | no |
| 2 | yes |
| 3 | no |
| 4 | yes |
| 5 | no |
| 6 | yes |

 

## Another Random Variable

We can define another property:

> Is the number greater than 3?

```python
def IsGreaterThan3(w):
    return 'yes' if w > 3 else 'no'
```

Now:

| Outcome \(w\) | IsGreaterThan3(w) |
|---|---|
| 1 | no |
| 2 | no |
| 3 | no |
| 4 | yes |
| 5 | yes |
| 6 | yes |

 

## 5. Unconditional Probability

Now we can finally compute probabilities involving random variables.

The most basic probability is:

$$
P(X = x)
$$

This means:

> Probability that random variable $\displaystyle X$ has value $x$.

 

### Example

What is:

$$
P(\text{IsEven} = \text{yes})
$$

We check all outcomes:

| Outcome | IsEven |
|---|---|
| 1 | no |
| 2 | yes |
| 3 | no |
| 4 | yes |
| 5 | no |
| 6 | yes |

The successful outcomes are:

$$
\{2,4,6\}
$$

There are 3 successful outcomes out of 6 total outcomes.

So:

$$
P(\text{IsEven} = yes) = \frac{3}{6} = 0.5
$$

 

## Python Implementation

```python
def unconditional_probability(
    Omega,
    P,
    VarX,
    x
):
    prob = 0.0

    for w in Omega:

        if VarX(w) == x:
            prob += P(w)

    return prob
```

 

## Understanding the Parameters

This function looks scary initially, but it is actually simple.

 

### Omega

The sample space.

```python
Omega = [1,2,3,4,5,6]
```

 

### P

The probability function.

```python
def P(w):
    return 1/6
```

 

### VarX

The random variable.

Example:

```python
IsEven
```

or:

```python
IsGreaterThan3
```

 

### x

The value we want to test.

Example:

```python
'yes'
```

 

## Running the Calculation

```python
result = unconditional_probability(
    Omega,
    P,
    IsEven,
    'yes'
)

print(result)
```

Output:

```python
0.5
```

 

## Step By Step Execution

The function loops over all outcomes.

 

### Iteration 1

```python
w = 1
```

Check:

```python
IsEven(1)
```

Result:

```python
'no'
```

Not equal to `'yes'`.

No probability added.

 

### Iteration 2

```python
w = 2
```

Check:

```python
IsEven(2)
```

Result:

```python
'yes'
```

Now we add:

```python
P(2)
```

which is:

```python
1/6
```

 

### Final Result

The successful outcomes are:

```python
2, 4, 6
```

So total probability becomes:

$$
\frac{1}{6}+\frac{1}{6}+\frac{1}{6}
=
\frac{3}{6}
=
0.5
$$

 

## 6. Joint Probability

$$
P(A \cap B)
$$

 

### Example

What is the probability that:

- the number is even
- AND greater than 3

The successful outcomes are:

$$
\{4,6\}
$$

So:

$$
P(\text{Even AND GreaterThan3})
=
\frac{2}{6}
=
0.3333
$$

 

## Python Implementation

```python
def unconditional_joint_probability(
    Omega,
    P,
    EventA
):
    prob = 0.0

    for w in Omega:

        okay = True

        for Var, val in EventA:

            if Var(w) != val:
                okay = False
                break

        if okay:
            prob += P(w)

    return prob
```

 

## Understanding EventA

This structure:

```python
[
    (IsEven, 'yes'),
    (IsGreaterThan3, 'yes')
]
```

means:

> We require BOTH conditions simultaneously.

 

## Running the Calculation

```python
event = [
    (IsEven, 'yes'),
    (IsGreaterThan3, 'yes')
]

result = unconditional_joint_probability(
    Omega,
    P,
    event
)

print(result)
```

Output:

```python
0.3333333333333333
```

 

# 7. Conditional Probability

Conditional probability asks:

> If we already know something happened, how likely is another event?

Mathematically:

$$
P(A \mid B)
$$

This reads:

> Probability of A given B.

 

## Formula

$$
P(A \mid B)
=
\frac{P(A \cap B)}{P(B)}
$$

 

## Example

Question:

> If the number is greater than 3, what is the probability that it is even?

The outcomes greater than 3 are:

$$
\{4,5,6\}
$$

Among those:

$$
\{4,6\}
$$

are even.

So:

$$
P(\text{Even} \mid \text{GreaterThan3})
=
\frac{2}{3}
=
0.6667
$$

 

## Python Implementation

```python
def conditional_probability(
    Omega,
    P,
    VarX,
    x,
    VarY,
    y
):

    numerator = unconditional_joint_probability(
        Omega,
        P,
        [(VarX, x), (VarY, y)]
    )

    denominator = unconditional_probability(
        Omega,
        P,
        VarY,
        y
    )

    if denominator == 0:
        return 0.0

    return numerator / denominator
```

 

## Running the Calculation

```python
result = conditional_probability(
    Omega,
    P,
    IsEven,
    'yes',
    IsGreaterThan3,
    'yes'
)

print(result)
```

Output:

```python
0.6666666666666666
```

 

# 8. Independence

Two events are independent if knowing one event does not affect the probability of the other.

Mathematically:

$$
P(A \cap B)
=
P(A)P(B)
$$

 

## Example

We know:

$$
P(\text{Even}) = 0.5
$$

and:

$$
P(\text{GreaterThan3}) = 0.5
$$

Multiplying:

$$
0.5 \times 0.5 = 0.25
$$

But earlier we computed:

$$
P(\text{Even AND GreaterThan3})
=
0.3333
$$

Since:

$$
0.3333 \neq 0.25
$$

the variables are NOT independent.

 

## Python Implementation

```python
def test_event_independence(
    Omega,
    P,
    EventA,
    EventB
):

    pab = unconditional_joint_probability(
        Omega,
        P,
        EventA + EventB
    )

    pa = unconditional_joint_probability(
        Omega,
        P,
        EventA
    )

    pb = unconditional_joint_probability(
        Omega,
        P,
        EventB
    )

    return abs(pab - pa * pb) < 1e-12
```

 

## Running the Calculation

```python
independent = test_event_independence(
    Omega,
    P,
    [(IsEven, 'yes')],
    [(IsGreaterThan3, 'yes')]
)

print(independent)
```

Output:

```python
False
```

 

## Final Thoughts

Probability gives us a simple way to describe uncertainty, compare events, and reason about outcomes with clear mathematical rules.
