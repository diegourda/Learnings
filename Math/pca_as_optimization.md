# PCA as an Optimization Problem

## Problem
Given centered data $X \in \mathbb{R}^{n \times d}$, find the direction of maximal variance.

## Optimization formulation
\[
\max_{\|v\|=1} \mathrm{Var}(Xv) = \max_{\|v\|=1} v^\top \Sigma v
\]

## Solution
This is a Rayleigh quotient.
The maximizer is the **top eigenvector** of the covariance matrix.

## Why this formulation matters
- Explains robustness issues
- Shows PCA is inherently second-order
- Connects to factor models and risk decomposition

## What breaks
- Heavy tails
- Nonlinear manifolds
- Time-varying covariance
