# Conditioning as Orthogonal Projection

## Core idea
Conditional expectation is not a formula — it is an **orthogonal projection** in an $L^2$ Hilbert space.

Given a random variable $X \in L^2$ and a sub-$\sigma$-algebra $\mathcal{G}$,  
$\mathbb{E}[X \mid \mathcal{G}]$ is the projection of $X$ onto the closed subspace of $\mathcal{G}$-measurable random variables.

## Why this matters
- Explains *why* conditional expectation minimizes MSE
- Clarifies martingales as projection-consistent processes
- Makes filtering, regression, and Kalman updates obvious

## Geometry
Let $H = L^2(\Omega, \mathcal{F}, \mathbb{P})$.
Let $H_{\mathcal{G}} \subset H$ be $\mathcal{G}$-measurable RVs.

Then:
\[
\mathbb{E}[X \mid \mathcal{G}] = \arg\min_{Y \in H_{\mathcal{G}}} \|X - Y\|_2
\]

## Failure modes
- Breaks outside $L^2$
- Conditioning on insufficient sigma-algebras causes bias
