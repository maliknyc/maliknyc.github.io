+++
title = 'Bonus Money Study Part 2: Long-Odds Hedging'
date = '2025-01-26'
math = true
+++
#### Levels 2 & 3

A common way to convert bonus money into real cash is to place the bonus bet on one side of a two-outcome event and simultaneously place a real-money hedge on the opposite side. When performed correctly, the conversion can be made completely risk-free.

Consider a two-outcome event with mutually exclusive and exhaustive outcomes \(A\) and \(B\). Suppose a bettor places bonus money of face value \(B>0\) on outcome \(A\) at decimal odds \(d_A>1\), and places a cash hedge of size \(H>0\) on outcome \(B\) at decimal odds \(d_B>1\).

Under the payout convention established in Part 1, if the bonus bet on \(A\) wins, it returns only the profit component \(B(d_A-1)\), while the cash hedge \(H\) is lost. Thus the net cash conversion if \(A\) occurs is

$$
C_A(H)=B(d_A-1)-H.
$$

If instead \(B\) occurs, the bonus bet loses, but the cash hedge wins and generates net profit \(H(d_B-1)\). Thus the net cash conversion if \(B\) occurs is

$$
C_B(H)=H(d_B-1).
$$

The bettor's objective is to choose \(H\) so as to maximize the guaranteed amount of cash extracted from the bonus, that is, to maximize

$$
\min\{C_A(H),\,C_B(H)\}.
$$

## The Risk-Free Hedge

Because \(C_A(H)\) is strictly decreasing in \(H\) and \(C_B(H)\) is strictly increasing in \(H\), the guaranteed conversion is maximized when the two outcomes yield the same cash amount. Thus the optimal hedge solves

$$
B(d_A-1)-H = H(d_B-1).
$$

Solving for \(H\), we obtain the unique risk-free hedge stake

$$
H^*=\frac{B(d_A-1)}{d_B}.
$$

Substituting \(H^*\) into either outcome gives the guaranteed cash conversion

$$
C^*=B(d_A-1)-H^*=H^*(d_B-1)=B(d_A-1)\left(1-\frac{1}{d_B}\right).
$$

Dividing by \(B\), the corresponding conversion rate is

$$
r^*=\frac{C^*}{B}=(d_A-1)\left(1-\frac{1}{d_B}\right).
$$

This is the standard formula for one-event bonus-bet conversion. It shows that the conversion rate depends only on the two quoted prices: the odds on the bonus side and the odds on the hedge side.

Recall that if the two prices are fair for a binary event, then \(1/d_A+1/d_B=1\). In that case, \(1-1/d_B=1/d_A\), allowing us to simplify the guaranteed conversion rate to

$$
r^*=(d_A-1)\frac{1}{d_A}=\frac{d_A-1}{d_A}.
$$

This is exactly the expected conversion rate of an unhedged bonus bet placed at fair odds. Thus, in a fair two-outcome market, single-event hedging transforms the expected value of the bonus bet into a certainty. In particular, under fair pricing, longer odds always improve the guaranteed conversion rate, since \(1-1/d_A\) is increasing in \(d_A\), with

$$
\lim_{d_A\to\infty}\frac{d_A-1}{d_A}=1.
$$

So in the no-vigorish benchmark, the guaranteed conversion can approach \(100\%\) of face value as the bonus-side odds become arbitrarily long.

## With Vigorish

In real sportsbook markets, the two-way odds are usually not fair. Let \(q_A=1/d_A\), \(q_B=1/d_B\), and define the two-way overround by \(h=q_A+q_B-1\). Then, \(h>0\) represents the bookmaker's margin, or *vigorish*. We can then rewrite the conversion rate as

$$
r^*=(d_A-1)\left(1-\frac{1}{d_B}\right)
=\left(\frac{1-q_A}{q_A}\right)(q_A-h).
$$

A useful decomposition is

$$
r^*=\frac{d_A-1}{d_A}-h(d_A-1),
$$

where the first term, \((d_A-1)/d_A\), can be treated as the "fair-odds benchmark," while the second term, \(h(d_A-1)\), is the reduction in conversion caused by vigorish. It follows immediately that, for fixed \(d_A\), a higher vigorish lowers the conversion rate, and that this penalty is larger for longer bonus-side odds.

## Optimal Bonus-Side Odds

A natural question that follows is whether, under a fixed level of vigorish, the bettor should simply place the bonus bet on the longest odds available. The answer is no. If \(h\) is held fixed, there is generally an interior optimum. We can maximize

$$
r^*(q_A)=\left(\frac{1-q_A}{q_A}\right)(q_A-h)
$$

with respect to \(q_A\):

$$
\frac{dr^*}{dq_A}=-1+\frac{h}{q_A^2}
=0.
$$

We solve to get \(q_A^*=\sqrt{h}\). Also notice that

$$
\frac{d^2r^*}{dq_A^2}=-\frac{2h}{q_A^3}<0,
$$

so this is the unique maximizer. Therefore, under a fixed two-way \(h\), the optimal implied probability on the bonus side is \(q_A^*=\sqrt{h}\), or equivalently,

$$
d_A^*=\frac{1}{\sqrt{h}}.
$$

Substituting \(q_A^*=\sqrt{h}\) into the conversion formula gives

$$
r_{\max}^*=(1-\sqrt{h})^2.
$$

This result formalizes an important practical point. Very short odds waste bonus value because the stake-not-returned structure is unfavorable there. But extremely long odds make the required hedge too expensive when factoring in the vigorish. The optimal one-event hedge lies at moderately long plus-money odds.

## Example

Consider a symmetric \(-110/-110\) market. In decimal form,

$$
d_A=d_B\approx 1.9091,
$$

so

$$
h=\frac{1}{1.9091}+\frac{1}{1.9091}-1\approx 0.047619.
$$

The fixed-overround optimum is then

$$
q_A^*=\sqrt{0.047619}\approx 0.2182,
\qquad
d_A^*=\frac{1}{\sqrt{0.047619}}\approx 4.58,
$$

which corresponds to approximately \(+358\) in American odds. The associated maximum guaranteed conversion rate is

$$
r_{\max}^*=(1-\sqrt{0.047619})^2\approx 0.611.
$$

So under a standard sportsbook-style two-way margin of roughly \(4.76\%\), the best possible one-event hedge converts about \(61.1\%\) of the bonus face value into risk-free cash.

## Capital Requirement

One final point is worth noting. Better conversion at longer bonus-side odds generally requires more real money to complete the hedge. Since

$$
H^*=\frac{B(d_A-1)}{d_B},
$$

the hedge stake can become quite large when \(d_A\) is large and \(d_B\) is correspondingly short. Thus, even when longer odds improve the conversion rate, they may be less practical for bettors with limited available cash.