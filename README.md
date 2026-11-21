# Two-sided density bounds for reversals of the three-halves prime window

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24410817.svg)](https://doi.org/10.5281/zenodo.24410817)

This result is now maintained in [prime-window-all-widths](https://github.com/leecrossley/prime-window-all-widths/tree/main/results/three-halves-reversal-density). This repository is archived and keeps its releases and DOI.

At dilation $b=3/2$, a reversal is a scale $y$ where the weighted sum of primes between $y$ and $2.25y$ overshoots its predicted size. Assuming the Riemann hypothesis (RH) and rational linear independence of the distinct positive ordinates of the nontrivial zeta zeros, reversals have a well-defined logarithmic density $\delta$, and this repository pins it between $10^{-10000}$ and $10^{-1012}$.

The lower bound shows that, under these hypotheses, reversals occupy a positive proportion of the logarithmic scale. The upper bound shows how small that proportion is. A [companion repository](https://github.com/leecrossley/three-halves-reversal-upper-density/tree/v1.0.0) bounds the upper logarithmic density by $10^{-232}$ under RH alone. Neither result locates the first reversal.

## Statement

Assume the Riemann hypothesis and rational linear independence of the distinct positive ordinates of the nontrivial zeta zeros. The $3/2$ weighted prime window overshoots its main term on a set with logarithmic density $\delta$ satisfying

$$10^{-10000}<\delta<10^{-1012}.$$

Fix $b=3/2$. Give each ordinary prime $p$ weight $(\log p)W_b(p/y)$, where

$$
W_b(t)=\begin{cases}
 b(1-1/t)&1 < t\le b,\\
 b^2/t-1&b < t < b^2,\\
 0&\text{otherwise}.
\end{cases}
$$

Write $D_b(y)=b(b-1)y\log b-\sum_p(\log p)W_b(p/y)$. A reversal means $D_b(y)<0$. Its frequency up to $X>1$ is

$$
d(X)=\frac{1}{\log X}\int_1^X {\bf1}_{D_b(y)<0}\thinspace\frac{dy}{y}.
$$

All logarithms are natural.

## How the proof goes

1. Under RH the normalised deficit $D_b(y)/\sqrt y$ is $-\Delta$ plus a sum of non-negative terms $a_\tau[1+\cos(\tau\log(by))]$ over the zeta zeros, up to $o(1)$. Here the $a_\tau>0$ are explicit summable coefficients with sum $L$, and $\Delta=L-2\sqrt b(\sqrt b-1)^2$ satisfies $0<\Delta<0.00163$. [PROOF.md](PROOF.md) gives the formulas.
2. Under independence, Kronecker's theorem makes the phases behave like independent uniform angles. The limiting distribution has no atom at zero, so the density $\delta$ exists.
3. **Upper bound.** In the limiting distribution, on the reversal event the terms from the first 5,000 zeros add up to at most $\Delta$. An exponential bound with $\lambda=1170000$ and Bessel function values gives $\delta<10^{-1012}$.
4. **Lower bound.** Hold the first 15,000 angles close to $\pi$, so that their terms add up to at most $0.0004$. Whatever the other angles, the remaining terms add at most $2(L-A_N)$, where $A_N$ is the sum of the first $N=15000$ coefficients, and the certificate proves the total stays below $\Delta$. This box of angles lies inside the reversal event and has volume above $10^{-10000}$.

The full argument is in [PROOF.md](PROOF.md).

## Verification

The first program isolates 15,000 consecutive positive ordinates with FLINT and computes both bounds in logarithms. The second verifies opposite signs of the completed zeta function on both sides of every supplied centre, then confirms the total count. It uses the unshifted ramp with a bounded series remainder, evaluates the Bessel upper bounds by positive series, and multiplies the lower box volume directly. Both use ball arithmetic.

```sh
python -m pip install -r requirements.txt
python verify.py
python independent.py
```

[Recorded runs](evidence/check.txt), [checksums](SHA256SUMS)

## Prior work

The existence argument belongs to the classical theory of prime races. Lamzouri studied large deviations for prime number races, and Zhao studied oscillation and bias for integrals of Mertens errors. The earlier result for this window establishes recurring conditional reversals. These two quantitative bounds apply to the specific $3/2$ ordinary-prime window. The literature checked yielded no earlier numerical interval for its reversal density. [Lamzouri](https://arxiv.org/abs/1103.0060), [Zhao](https://arxiv.org/html/2411.18903v2), [Earlier oscillation statement](https://github.com/leecrossley/prime-band-three-halves-oscillation/tree/v1.0.1)
