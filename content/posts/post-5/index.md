+++
title = '[BBM 4] The Simulation Process'
date = '2025-01-03'
math = true
draft = true
+++
#### Levels 2 & 3

# Betting Behavior Methodologies 4: The Simulation Process

## A Single Simulation

**The main limitation** of our generalized formula with respect to modeling "irrational" betting behavior is that it still maximizes utility in a "rational" way, and thus, like the classical Kelly, will still **always** advise against placing a nonzero wager on a negative EV bet. However, one way we can effectively loosen this restriction in our simulations is through probability weighting or by introducing some distinction between "perceived" probabilities and actual probabilities. In accordance with our established decision framework, the simulation tests a single chosen bet against a bet sizing strategy each time we run it. Let's walk through the process for a **single** simulation. Before initiating the simulations, several critical parameters are established:

- **\( N \)**: The total number of independent betting sequences to be simulated to ensure statistical significance.

- **\( T \)**: The maximum number of bets allowed per simulation to prevent indefinite betting sequences.
- **\( L \)**: The wealth level at which the bettor is considered bankrupt, terminating the sequence.
- **\( W_0 \)**: Starting wealth of the bettor.
- **\( \gamma \)**: The investor's degree of risk aversion, influencing the optimal betting fraction.
- **\( p_{\text{perceived}} \)**: The weighted, subjective belief about the likelihood of the bet winning.
- **\( p_{\text{actual}} \)**: The true likelihood of the bet winning.
- **\( b \)**: The net odds of the bet offering, i.e., the potential profit per unit wagered.

Each simulation encapsulates a sequential series of bets where the proportion of the current wealth \( W \) that the bettor allocates to bet, \( f^* \), is based on \( p_{\text{perceived}} \) and aligns with their risk preferences as characterized by \( \gamma \):

$$
f^* = \frac{\left(\frac{p_{\text{perceived}}\cdot b}{1-p_{\text{perceived}}}\right)^\frac{1}{\gamma}-1}{b+\left(\frac{p_{\text{perceived}}\cdot b}{1-p_{\text{perceived}}}\right)^\frac{1}{\gamma}}
$$

For each betting round, the amount to wager is computed as a fraction of the current wealth:
\( A_t = W_t \cdot f^* \)
where \( W_t \) is the wealth before the \( t \)-th bet. The outcome of the bet is determined based on the **actual** probability of winning, \( p_{\text{actual}} \). A uniformly distributed random variable \( U \sim \mathcal{U}(0,1) \) can be generated to decide the outcome. If \( U < p_{\text{actual}} \), the bet is won; if else, the bet is lost. Depending on the outcome, the wealth is updated as follows:

$$
W_{t+1} = \begin{cases}
    W_t \cdot (1+f^*\cdot b) & \text{if win,}\\
    W_t \cdot(1-f^*) & \text{if lose.}
\end{cases}
$$

The updated wealth \( W_{t+1} \) can be appended to a wealth history, \( \mathcal{W} = \{W_0, W_1, W_2,..., W_{t+1}\} \), allowing us to track and analyze our simulation outcomes at a granular level. We can also check for peak and minimum wealth levels, where \( W_{peak} = \text{max}(W_{peak}, W_{t+1}) \) and \( W_{min} = \text{min}(W_{min}, W_{t+1}) \). At each step, the simulation should check for bankruptcy: if \( W_{t+1} \leq L \), the simulation is marked as bankrupt, and the betting loop terminates.

After \( T \) bets or upon bankruptcy, the following metrics can be recorded:

- **\( W_T \)**: The wealth level at termination.

- **\( W_{\text{peak}} \)**: The highest wealth achieved during the simulation.
- **\( W_{\text{min}} \)**: The lowest wealth reached during the simulation.
- **\( T_f \)**: Total number of bets before termination.
- **\( \text{Ruin}^{(i)} \)**: Whether the simulation ended in ruin.
- **\( \mu_{\ln(W)} \)**: The mean log-wealth, which can also be represented as:
    $$
    \mu_{\ln(W)} = \frac{1}{T_f}\sum_{k=1}^{T_f}\ln(W_k)
    $$
- **\( \sigma_{\ln(W)} \)**: The standard deviation of log-wealth, which can also be represented as:
    $$
    \sigma_{\ln(W)} = \sqrt{\frac{1}{T_f} \sum_{k=1}^{T_f} \left( \ln(W_k) - \mu_{\ln (W)} \right)^2}
    $$
- **\( \beta \)**: The slope of log-wealth, which can be determined by fitting a linear regression model to the log-transformed wealth history.
    $$
    \ln(W_k) = \beta k + \alpha + \epsilon_k \quad \Rightarrow \quad \beta = \frac{\ln(W_k) - \alpha - \epsilon_k}{k}
    $$
    where \( \alpha \) is the intercept and \( \epsilon_k \) represents residuals.

## Multiple Simulations

To obtain statistically significant results, the simulation should be executed \( N \) times, from \( i=1 \) to \( N \), each being independent betting sequences with the same parameters. We can establish a counter variable, \( C_{\text{ruin}} \), that increments by one each time a simulation results in bankruptcy to track the number of simulations that terminate before reaching \( T \) bets. Let's look at some aggregate statistics we can compute.

- **\( P_{\text{ruin}} \)**: The likelihood of a bettor reaching bankruptcy under the given bet, betting strategy, and risk preferences.
    \(
    \left(\dfrac{C_{\text{ruin}}}{N}\right) \cdot 100\%
    \)

- **\( \overline{W}_T \)**: The mean wealth achieved at the conclusion of all simulations.
    \(
    \dfrac{1}{N}\sum_{i=1}^{N} W_T^{(i)}
    \)

- **\( \overline{W}_{\text{peak}} \)**: The typical maximum wealth attained across all simulations.
    \(
    \dfrac{1}{N}\sum_{i=1}^{N} W_{\text{peak}}^{(i)}
    \)

- **\( \overline{W}_{\text{min}} \)**: The typical minimum wealth attained across all simulations.
    \(
    \dfrac{1}{N}\sum_{i=1}^{N} W_{\text{min}}^{(i)}
    \)

- **\( W_{T}^{max} \)**: The maximum wealth achieved across all simulations.
    \(
    \underset{1 \leq i \leq N}{\text{max}} \, W_T^{(i)}
    \)

- **\( \overline{\mu}_{\ln(W)} \)**: The mean of log-wealth.
    \(
    \dfrac{1}{N} \sum_{i=1}^{N} \mu_{\ln(W)}^{(i)}
    \)

- **\( \overline{\sigma}_{\ln(W)} \)**: The standard deviation of log-wealth.
    \(
    \sqrt{\dfrac{1}{N} \sum_{k=1}^{N} \left( \ln(W_k) - \mu_{\ln W} \right)^2}
    \)

- **\( \overline{\beta} \)**: The average slope of log-wealth.
    \(
    \dfrac{1}{N} \sum_{i=1}^{N} \beta^{(i)}
    \)

- **\( \overline{T}_{\text{ruin}} \)**: The average time to ruin across all simulations.
    $$
    \dfrac{1}{C_{\text{ruin}}}\sum_{i=1}^{N} T_{\text{ruin}}^{(i)} \quad \text{for } \text{Ruin}^{(i)} = \text{True}
    $$

## Incorporating Perceived Probability Weighting

The separation between \( p_{\text{perceived}} \) and \( p_{\text{actual}} \) is a **crucial** component that allows us to model and study "irrational" betting behavior (i.e., bet sizing behavior when wagering nonzero amounts on negative EV bets). Even when the bet's expected value is negative, the *perceived* odds can lead to the belief that there is still positive expected value, creating a framework where the simulated bettor still places nonzero bets in a "risk-averse" way due to their incorrect assessment of their edge. There can be a multitude of approaches to deciding \( p_{\text{perceived}} \), such as choosing some desired fixed probability that deviates from \( p_{\text{actual}} \), applying some scalar to \( p_{\text{actual}} \), or, as we will go over here, applying Prelec's probability weighting function to \( p_{\text{actual}} \). More specifically, we can use our *dependent weighting by complementarity* strategy to weigh only the probability of gain and set the perceived probability of loss as the complement:

$$
p_{\text{perceived}} = \exp\left(-(-\ln(p_{\text{actual}}))^{\alpha}\right)
$$

where \( \alpha \in (0,1) \) is the probability weighting coefficient. The perceived probability of loss is then \( 1 - p_{\text{perceived}} \). Subsequently, we can test how individuals with different combinations of \( \alpha \) and \( \gamma \) might behave and perform given specific bets.

## Visualizing and Interpreting Simulation Results

Alongside the aggregate statistics, we can also employ various visualization techniques, such as wealth progression plots and a final wealth distribution histogram. For the purpose of demonstration, let's look at the simulation results for several combinations of \( \alpha \) and \( \gamma \) given bet parameters modeled after a roulette "Straight Up" bet, which typically has a 1 in 38 chance of hitting and pays out 35 to 1, yielding approximately a \( -5.26\% \) edge. In other words, the **expected loss** per \$1 bet is approximately \$0.0526. In principle, all bettors with \( \gamma \geq 0 \) and \( \alpha = 1 \) (i.e., "rational" bettors) should refrain from playing such a bet.

For consistency, let's keep the following simulation parameters fixed across all cases:
- \(N = 1,000\)
- \( T = 10,000 \)
- \( L = $10 \)
- \( W_0 = $1,000 \)
- \( p_{\text{actual}} = 1/38 \)
- \( b = 35 \)

 We will also be using \( p_{\text{perceived}} = \exp\left(-\left(-\ln(p_{\text{actual}})\right)^{\alpha}\right) \) to determine the perceived probabilities. Because we have yet to obtain empirical evidence on the "typical" ranges for \( \alpha \) and \( \gamma \), for interpretation purposes, we could keep on hand \( \alpha = 1 \), where the bettor has **no** probability distortion, and \( \gamma = 1 \), where the bettor has a logarithmic risk profile and maximizes their geometric rate of growth, as reference points. From those points, we can establish a few tentative and heuristic ranges to categorize the other levels of \( \gamma \) and \( \alpha = 1 \). Values of \( \gamma \) between 0 and 1 can be considered "low" levels of risk-aversion; values between 1 and 2 can represent "high" levels of risk-aversion, and values above 2 can represent "very high" levels of risk-aversion. For the same heuristic purposes, values of \( \alpha \) equal to or below 0.8 can be considered "extreme," values between 0.81 and 0.85 can qualify as "very high," values between 0.86 and 0.9 can qualify as "high," values between 0.91 and 0.95 can qualify as "moderate," and values between 0.96 and 1 can be deemed "mild."

As can be observed in the output table below, the often dramatic jump in \(P_{\text{ruin}}\) from \(\alpha = 0.98\) to \(\alpha = 0.93\) might call for a more restricted range of meaningful \(\alpha\)'s. A clear and unsurprising pattern materializes in our results: Higher \(\alpha\)'s and \(\gamma\)'s generally lead to higher peak wealth levels, but at the cost of significantly higher rates of ruin. As can be expected, more conservative strategies yield better **averages** for this negative EV bet; however, the higher peaks produced by the more aggressive methods might actually be of some value given shorter time horizons, especially if a bettor has a specific **target wealth** in mind. Right now, the average final wealth levels alone seem to be ample evidence of the rather intuitive fact that betting less on unprofitable bets will yield all-around better long-term results. 

![Image alt](images/sim_outputs.png)

Please see below for a bunch of the visualizations from the simulation runs:

![Image alt](images/high_log_WP.png)
![Image alt](images/high_log_log_WP.png)
![Image alt](images/high_log_dist.png)
![Image alt](images/low_log_WP.png)
![Image alt](images/low_log_log_WP.png)
![Image alt](images/low_log_dist.png)
![Image alt](images/RA_high_WP.png)
![Image alt](images/RA_high_log_WP.png)
![Image alt](images/RA_high_dist.png)
![Image alt](images/RA_low_WP.png)
![Image alt](images/RA_low_log_WP.png)
![Image alt](images/RA_low_dist.png)

