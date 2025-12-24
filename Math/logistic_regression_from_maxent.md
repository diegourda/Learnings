# Logistic Regression from Maximum Entropy

## Setup
We want the least-informative distribution consistent with observed constraints.

## Constraints
- $\mathbb{E}[y x]$ is fixed
- Labels are binary

## Result
Solving the constrained entropy maximization yields:
\[
P(y=1 \mid x) = \sigma(w^\top x)
\]

## Interpretation
Logistic regression is not a heuristic —
it is the **most unbiased classifier** under linear constraints.

## Why this matters
- Clarifies regularization
- Explains exponential families
- Links statistics and information theory
