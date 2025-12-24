# HJB Equation from Dynamic Programming

## Setup
Controlled SDE:
\[
dX_t = b(X_t, u_t)dt + \sigma(X_t)dW_t
\]

## Dynamic programming principle
Optimal value over $[t, T]$ equals:
- immediate reward
- plus optimal continuation

## Result
Taking limits yields the HJB PDE.

## Why this matters
- Shows optimal controls are local
- Explains feedback policies
- Foundation of stochastic control
