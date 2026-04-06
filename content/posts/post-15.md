+++
title = 'Bonus Money Study Part 3: Diversification
date = '2026-04-05'
math = true
+++
#### Levels 2 & 3

# Diversification Across Many Independent Bonus Wagers

The single-event hedge studied in the previous post produces an exact risk-free conversion by supplementing the bonus wager with a real-money hedge. A different benchmark is obtained if the bettor instead spreads the bonus funds across many independent bonus wagers. This doesn't, by itself, create a risk-free payoff in finite cases, but it does reduce volatility and clarifies the sense in which bonus money can become more cash-like under diversification.

Let a total bonus amount \(B>0\) be allocated across \(N\) independent bonus wagers. Write \(b_i \geq 0\) for the face value allocated to wager \(i\), where \(\sum_{i=1}^N b_i = B\).
Let wager \(i\) be placed at decimal odds \(d_i>1\), and let \(E_i\) denote the event that wager \(i\) wins. As before, the cash conversion from wager \(i\) is \(Y_i = b_i(d_i-1)\mathbf{1}_{E_i}.\) The total cash conversion across all \(N\) wagers is therefore \(S_N=\sum_{i=1}^N Y_i.\)
Assuming the wagers are independent and fairly priced, so that \(\Pr(E_i)=1/d_i\),
we have \(\mathbb{E}[Y_i]=b_i(d_i-1)/d_i\) and \(\operatorname{Var}(Y_i)=b_i^2(d_i-1)^3/d_i^2\).
By linearity of expectation and independence,

$$
\mathbb{E}[S_N]
=
\sum_{i=1}^N b_i\frac{d_i-1}{d_i}
$$

and

$$
\operatorname{Var}(S_N)
=
\sum_{i=1}^N b_i^2\frac{(d_i-1)^3}{d_i^2}.
$$

Thus, we can notice that diversification doesn't generate expected conversion on its own. The expected conversion rate is simply

$$
\frac{\mathbb{E}[S_N]}{B}
=
\sum_{i=1}^N \frac{b_i}{B}\cdot \frac{d_i-1}{d_i},
$$

which is a weighted average of the individual fair conversion rates. In particular, if all wagers are placed at the same odds \(d\), then \(\mathbb{E}[S_N]=B(d-1)/d\), regardless of how the bonus is split. Diversification simply changes the risk.

## Equal-Odds Benchmark

Suppose now that all \(N\) wagers are placed at the same decimal odds \(d>1\). Then \(\mathbb{E}[S_N]=B(d-1)/d\)
and \(\operatorname{Var}(S_N)
=(d-1)^3/(d^2)\sum_{i=1}^N b_i^2\).
I'll make the **claim** that among all allocations \((b_1,\dots,b_N)\) satisfying \(\sum_{i=1}^N b_i=B\), the variance of \(S_N\) is minimized by equal splitting:

$$
b_1=\cdots=b_N=\frac{B}{N}.
$$

The **proof** is as follows. Since \((d-1)^3/d^2>0\), minimizing \(\operatorname{Var}(S_N)\) is equivalent to minimizing \(\sum_{i=1}^N b_i^2\) subject to \(\sum_{i=1}^N b_i=B\). By Cauchy--Schwarz,

$$
\left(\sum_{i=1}^N b_i\right)^2 \leq N\sum_{i=1}^N b_i^2,
$$

so

$$
\sum_{i=1}^N b_i^2 \geq \frac{B^2}{N},
$$

with equality if and only if \(b_1=\cdots=b_N=B/N\). ∎

Under this equal-split allocation, \(b_i=B/N \quad (i=1,\dots,N)\), we obtain \(\mathbb{E}[S_N]=B(d-1)/d\) and \(\operatorname{Var}(S_N)=B^2(d-1)^3/(Nd^2)\). Thus, for fixed common odds, diversification reduces variance at rate \(1/N\) while leaving expected conversion unchanged. Equivalently, the standard deviation falls at rate \(N^{-1/2}\).

## Concentration Under Diversification

The preceding formulas imply that, under equal splitting and fixed common odds \(d\), the realized conversion becomes increasingly concentrated around its mean as the number of independent wagers grows.

More formally, I'm **claiming** that if \(b_i=B/N\) for all \(i\) and all wagers are placed at the same fair odds \(d>1\), then

$$
S_N \xrightarrow{p} B\frac{d-1}{d}
\qquad \text{as } N\to\infty.
$$

The **proof** is by Chebyshev's inequality, where for every \(\varepsilon>0\),

$$
\Pr\left(\left|S_N-B\frac{d-1}{d}\right|>\varepsilon\right)
\leq
\frac{\operatorname{Var}(S_N)}{\varepsilon^2}
=
\frac{B^2(d-1)^3}{N d^2 \varepsilon^2}.
$$

The right-hand side converges to \(0\) as \(N\to\infty\), so the claim follows. ∎

This result gives a precise sense in which diversification makes bonus money more cash-like: with enough independent wagers, the realized conversion becomes nearly deterministic. But it's important to be clear about what it converges to. For fixed \(d\), the limit is \(B(d-1)/d,\) not \(B\). Thus diversification alone makes bonus money approach a certain discounted cash value, not full face value.

## Approaching Full Cash Value

To make diversified bonus money approach full cash value, the odds themselves must also increase. Suppose the odds are allowed to depend on \(N\), so that each of the \(N\) equal-split wagers is placed at odds \(d_N>1\). Then \(\mathbb{E}[S_N]=B(d_N-1)/(d_N)\) and \(\operatorname{Var}(S_N)=B^2(d_N-1)^3/(N d_N^2)\).
If \(d_N\to\infty\) and \(d_N/N\to0\), then \(\mathbb{E}[S_N]\to B\) and \(d_N/N\to0\). Hence

$$
S_N \xrightarrow{p} B.
$$

So, in an idealized setting with sufficiently divisible bonus credit and sufficiently many independent opportunities, bonus money can be made arbitrarily close to cash in both mean and risk. Still, this is just a theoretical benchmark. For any finite \(N\), diversification alone doesn't produce an exact risk-free conversion, since \(\operatorname{Var}(S_N)>0\) whenever each wager retains positive win and loss probability.