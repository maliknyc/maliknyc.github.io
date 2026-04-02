+++
title = 'Bonus Money Study: Part 1'
date = '2025-01-25'
math = true
+++
#### Levels 2 & 3

# Introduction

Most people fall into one of two camps when they see a sportsbook promotion. The naïve bettor thinks they have stumbled into a windfall. The skeptical bettor thinks that they are being taken for a ride. Both reactions are understandable, but neither is particularly useful. Bonus bets occupy a more interesting position than either camp typically appreciates—they are not cash, but they are not nothing. Bonus bets return winnings but not stake, which means their value is not fixed; it is a function of how they are used. This subtlety is easy to miss, especially when ads dangle offers like "bet $5, get $200 in bonus bets," or promise to refund a losing first wager in promotional credit. Once the mechanics are understood, we can study how much of this "bonus money" can be extracted as cash, and with as little risk as possible.

# Institutional Setup and Notation

For most of these posts, we will focus on a specific class of promotional credits that are commonly referred to as *bonus money*. The key contractual feature of the instrument studied here is: when the promotional credit is used to place a wager and that wager wins, the bettor receives only the *profit* from the wager, not the promotional stake itself. To avoid ambiguity, I will use the term *bonus money* to mean exactly that. Formally, a bonus amount \(B>0\) is a non-withdrawable credit that may be staked on an admissible wager, but which is extinguished after use regardless of the wager's outcome. If the wager loses, the bettor receives nothing. If the wager wins at decimal odds \(d>1\), the bettor receives the profit component \(B(d-1)\) in cash or cash-equivalent withdrawable balance, but does not recover the original bonus stake \(B\).

This definition intentionally abstracts from several institutional details that vary across sportsbooks, such as expiration dates, minimum-odds requirements, playthrough requirements, stake caps, market restrictions, and payout rounding conventions. These frictions may matter in practice, but they are secondary to the central mechanical feature studied here: bonus money pays winnings but not stake. Unless otherwise stated, the analysis below assumes that the bonus funds may be used on any eligible market and that any winnings produced by the bonus bet are withdrawable as ordinary cash. Promotions that initially take some other form—for example, a "second-chance" refund on a losing first wager—still fall within this framework once the refund is issued in the form of bonus money.

## Odds, Events, and Payout Conventions

All odds will be written in decimal form. If a wager is placed at decimal odds \(d>1\), then a *cash* stake of size \(W>0\) returns \(Wd\) upon winning, which consists of the returned stake \(W\) plus profit \(W(d-1)\). If the wager loses, the bettor receives \(0\), so the net profit from a cash wager is

$$
\pi_{\text{cash}} =
\begin{cases}
W(d-1), & \text{if the wager wins},\\
-W, & \text{if the wager loses}.
\end{cases}
$$

By contrast, if a *bonus* stake of face value \(B>0\) is used at the same decimal odds \(d\), the bettor receives only the profit component if the wager wins. Thus the realized cash conversion from a bonus wager is

$$
Y =
\begin{cases}
B(d-1), & \text{if the wager wins},\\
0, & \text{if the wager loses}.
\end{cases}
$$

\(Y\) is our main object of interest in most of what follows. It is a measurement of how much real cash is extracted from a face value \(B\) of promotional credit. Let \(E\) denote the event on which the wager is placed, and let \(p=\Pr(E)\) be the bettor's assessed probability that the wager wins. Then the expected cash conversion from a bonus wager is

$$
\mathbb{E}[Y] = p\,B(d-1).
$$

If the bettor takes the sportsbook's price as *fair*, then \(p=1/d\), in which case

$$
\mathbb{E}[Y] = \frac{1}{d}B(d-1) = B\frac{d-1}{d}.
$$

Notice that for an ordinary cash wager placed at fair odds, the expected total return equals the stake \(W\), regardless of the odds. For a bonus wager, however, the expected cash conversion \(B(d-1)/d\) depends on \(d\), and increases with the length of the odds. In particular,

$$
\lim_{d\to\infty} B\frac{d-1}{d} = B.
$$

Thus, under fair pricing, a bonus bet used on longer odds converts a larger fraction of its face value into expected cash.

## Implied Probabilities and Vigorish

For a decimal price \(d\), the corresponding implied probability is \(q=1/d\). In a two-outcome market with decimal odds \(d_A\) and \(d_B\), the bookmaker's overround (or vigorish) is reflected in the fact that

$$
\frac{1}{d_A} + \frac{1}{d_B} \geq 1.
$$

Equality corresponds to a no-vigorish or "fair" market, while strict inequality corresponds to positive bookmaker margin.

It is useful to distinguish between two separate notions of value: (1) the *face value* \(B\) of the promotional credit, and (2) the *cash conversion value*, meaning the amount of withdrawable money generated by using that credit in a wager or collection of wagers. These two quantities are not the same. The face value \(B\) is fixed by the promotion, but the cash conversion value depends on the odds, the hedging method, the amount of vigorish embedded in the prices, and the bettor's willingness to bear risk.

## Hedging Objective

My objective is to maximize nominal winnings conditional on a particular bet winning. Instead, I want to study how a bettor can convert bonus money into real cash as efficiently and safely as possible. More precisely, suppose a bettor receives bonus credit of face value \(B\). A *conversion strategy* is any admissible collection of wagers, possibly supplemented by real-money hedges, that uses the bonus credit and produces a random cash outcome \(C\). The problem is then to study either

1. the expected conversion \(\mathbb{E}[C]\),
2. the risk of conversion, measured for example by \(\mathrm{Var}(C)\), or
3. risk-free or nearly risk-free conversion schemes that make \(C\) constant or close to constant across outcomes.

This framing is intentionally broad enough to include a single unhedged bonus wager, a conventional hedge against the opposite side of the same event, or a more elaborate structure built from many wagers spanning a larger outcome space.

# A Single Bonus Bet

The simplest possible use of bonus money is a single wager on a single event. Let \(B>0\) denote the face value of a single unit of bonus money, and let a wager be placed on an event \(E\) at decimal odds \(d>1\). Let

$$
\mathbf{1}_E =
\begin{cases}
1, & \text{if } E \text{ occurs},\\
0, & \text{otherwise}
\end{cases}
$$

be the indicator that the wager wins. Then, the realized cash conversion from the bonus wager is

$$
Y = B(d-1)\mathbf{1}_E.
$$

Equivalently,

$$
Y =
\begin{cases}
B(d-1), & \text{with probability } p,\\
0, & \text{with probability } 1-p,
\end{cases}
$$

where \(p=\Pr(E)\) is the bettor's assessed win probability. Note that this formulation is preferable to treating a losing bonus wager as generating a payoff of \(-B\). The bettor does not lose cash when the bonus bet loses; rather, the opportunity to convert the promotional credit is lost. Since the object of interest is the amount of real money extracted from the bonus, \(Y\) is naturally defined as a nonnegative cash-conversion variable.

Although longer odds improve expected conversion, they also make conversion more volatile. Computing the variance of \(Y\) gives us

$$
\mathrm{Var}(Y)
= p\bigl(B(d-1)\bigr)^2 - \bigl(pB(d-1)\bigr)^2
= p(1-p)B^2(d-1)^2.
$$

Under fair pricing (\(p=1/d\)), this simplifies to

$$
\mathrm{Var}(Y)
=
\frac{1}{d}\left(1-\frac{1}{d}\right)B^2(d-1)^2
=
B^2\frac{(d-1)^3}{d^2}.
$$

So a single unhedged bonus bet presents a basic tradeoff: longer odds raise the expected amount of cash that can be extracted, but they also raise the variance of the realized conversion.

## Expected Conversion Value

Recall that the expected cash conversion from the single bonus bet is \(\mathbb{E}[Y] = p\,B(d-1)\). Also recall that under fair sportsbook pricing, \(\mathbb{E}[Y]=B(d-1)/d\). This expression has several immediate implications.

First, for fixed \(B\), the expected conversion value is strictly increasing in \(d\). A short-odds bonus bet converts only a small fraction of its face value in expectation, while a long-odds bonus bet converts a larger fraction.

Second, the expected conversion value is always strictly less than \(B\) for finite \(d\), but approaches \(B\) as \(d\to\infty\). Thus a bonus bet never quite becomes equivalent to cash under finite odds, though long odds can make it close in expected-value terms.

Third, this differs fundamentally from a fair cash wager. A cash stake of size \(W\) at fair odds always has expected total return \(W\), independent of the odds. The dependence of \(\mathbb{E}[Y]\) on \(d\) is therefore not a generic betting phenomenon; it is a direct consequence of the stake-not-returned structure of bonus money.

## Risk of a Single Bonus Bet

Although longer odds improve expected conversion, they also make conversion more volatile. Since

$$
Y =
\begin{cases}
B(d-1), & \text{with probability } p,\\
0, & \text{with probability } 1-p,
\end{cases}
$$

we have

$$
\mathrm{Var}(Y)
= p\bigl(B(d-1)\bigr)^2 - \bigl(pB(d-1)\bigr)^2
= p(1-p)B^2(d-1)^2.
$$

Under fair pricing, where \(p=1/d\), this simplifies to

$$
\mathrm{Var}(Y)
=
\frac{1}{d}\left(1-\frac{1}{d}\right)B^2(d-1)^2
=
B^2\frac{(d-1)^3}{d^2}.
$$

So a single unhedged bonus bet presents a basic tradeoff: longer odds raise the expected amount of cash that can be extracted, but they also raise the variance of the realized conversion. This tradeoff is what motivates the hedging methods studied in the sections that follow.

## Conversion Rate

For later use, it is also helpful to define the *conversion rate* of a strategy as the ratio of realized or expected cash extracted to the face value of the bonus credit. For a single bonus bet, the expected conversion rate is

$$
\rho(d,p) = \frac{\mathbb{E}[Y]}{B} = p(d-1).
$$

Under fair pricing,

$$
\rho(d) = \frac{d-1}{d}.
$$

This gives a convenient normalized measure of how efficiently a bonus wager transforms promotional credit into real cash.