# Stability of Linear ODEs and Why Discretization Lies

## Continuous system
\[
\dot{x} = Ax
\]

Stability is determined entirely by the eigenvalues of $A$.

## Discrete trap
Euler discretization:
\[
x_{k+1} = (I + hA)x_k
\]

A stable continuous system can become unstable numerically.

## Implication
Numerics can introduce **fake dynamics**.

## Why quants should care
- Policy iteration instability
- Exploding controls
- Misleading backtests
