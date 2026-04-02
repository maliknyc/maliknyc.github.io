+++
title = '[BBM 2] Probability Weighting Quiz'
date = '2025-01-03'
math = true
draft = true
+++
#### Levels 2 & 3

# Betting Behavior Methodologies 2: Probability Weighting Quiz

Building onto the [CRRA Quiz](https://maliknyc.github.io/karmagambler.github.io/posts/post-2/), we might want to assess how susceptible someone is to probability weighting: the tendency to overweight low probabilities and underweight large probabilities. For now, we'll focus on binary gambles with risky options that offer low-probability gains and high-probability losses. In other words, we're essentially attempting to explain "favorite-longshot bias" &mdash; an observed tendency for bettors to overvalue heavy underdogs and undervalue heavy favorites (Griffith 1949). Our setup might also bring to mind concepts from Salience Theory, which suggests that decision-makers overweight extremely &mdash; or "saliently" &mdash; unlikely events if they are aware of their possibility (i.e. we react more to possibility than we do to probability) (Bordalo 2012). The participant's baseline preferences will be modeled using the CRRA utility function and estimated risk aversion coefficient, \(\gamma\), elicited in the prior section. To capture the non-linear perception of probabilities, we will employ Prelec's probability weighting function:
$$
w\left(p\right)=\exp\left(-\left(-\ln p\right)^{\alpha}\right)
$$
Where:
- \( p \in (0, 1) \): the objective probability.
- \( \alpha > 0\): the degree of probability distortion (or the **curvature parameter**).
When \( \alpha < 1 \), the function overweights low probabilities and underweights high probabilities. When \( \alpha = 1 \), the function causes no probability distortion. When \( \alpha > 1 \), the function underweights low probabilities and overweights high probabilities. Because empirical estimates suggest an s-shape, for now, we will constrain \( \alpha \) to (0, 1).

Our goal is to integrate the weighting function into CRRA utility calculations to create a more comprehensive framework that incorporates the phenomenon of probability weighting.

Let us establish a particular decision framework that tests our aforementioned focus. Participants begin with an initial wealth of $1,000. In each round of the quiz, participants are presented with two options:

- **Option A:** A sure gain of $0. In other words, no bet.
- **Option B:** A 2% probability of gaining $1,000 and a 98% probability of losing \(X^*\).

Similar to our previous quiz, both the initial wealth amount and the sure gain amount are arbitrary and chosen for consistency and interpretability. The probability distribution is chosen to produce an option that offers a low-probability gain prospect and a high-probability loss prospect, similar to a "longshot" bet or a lottery scenario where \(X^*\) is the price of a lottery ticket a participant is willing to pay. To finish constructing our quiz, we will have to compute the \( X^* \) values where the participant will be indifferent between Option A and Option B at different combinations of \( \alpha \) and \( \gamma \).

First, let us examine two strategies for applying probability weighting in binary gambles: (a) independently applying the weighting function to both outcomes and (b) applying the weighting function to one probability and deriving the other as its complement.

### (a) Independent Weighting of Both Probabilities
Here, the weighting function is independently applied to both the probability of gain and the probability of loss as follows:
$$
w_{gain} = w(p_{gain}), \quad w_{loss} = w(p_{loss})
$$

Using these weighted probabilities in a risky utility calculation gives us the expected weighted utility:
$$
\mathbf{E}[u(W)] = w_{gain} \cdot U(W_{gain}) + w_{loss} \cdot U(W_{loss})
$$
In the context of our decision framework, this becomes:
$$
\mathbf{E}[u(W)] = \exp\left(-\left(-\ln 0.02\right)^{\alpha}\right) \cdot 
\frac{(2,000)^{1-\gamma} - 1}{1 - \gamma} + \exp\left(-\left(-\ln 0.98\right)^{\alpha}\right)
\cdot \frac{(1,000-X^*)^{1-\gamma} - 1}{1 - \gamma}
$$
When put into practice, this approach seems to run into a **plethora of issues**. To start, since Prelec's function is non-linear, it is **typically true** that \(w_{gain} + w_{loss} \neq 1\). This disrupts the coherence of the probability space but is likely not a direct deal-breaker for modeling irrational probability perceptions. We will also encounter many undefined or incoherent solutions for \(X^*\), especially at the "higher" combinations of \(\alpha\) and \(\gamma\) where \(W_{loss} = W_0 - X^* \geq 0\) and the \(X^*\) values turn negative. Let us go through an example calculation of \(X^*\) where \(\alpha = 0.25\) and \(\gamma = 0.7\). First, we can establish our CRRA utility function:
$$
u(w) = \frac{w^{0.3}-1}{0.3}
$$
Then, we can compute the utility of Option A (the safe option):
$$
u(1,000) = \frac{1,000^{0.3}-1}{0.3}
$$
The expected utility of Option B will be:
$$
\mathbf{E}[u(W)] = \exp\left(-\left(-\ln 0.02\right)^{0.25}\right) \cdot 
\frac{(2,000)^{0.3} - 1}{0.3} + \exp\left(-\left(-\ln0.98\right)^{0.25}\right)\cdot \frac{(1,000-X^*)^{0.3} - 1}{0.3}
$$
Setting the utility of Option A equal to the expected utility of Option B yields:
$$
\frac{1,000^{0.3}-1}{0.3} = \exp\left(-\left(-\ln 0.02\right)^{0.25}\right) \cdot 
\frac{(2,000)^{0.3} - 1}{0.3} + \exp\left(-\left(-\ln0.98\right)^{0.25}\right)\cdot \frac{(1,000-X^*)^{0.3} - 1}{0.3}
$$
Simplifying and solving for \(X^*\):
\[
1,000^{0.3} - 1 - \exp\left(-\left(-\ln 0.02\right)^{0.25}\right) \cdot (2,000^{0.3} - 1) = \exp\left(-\left(-\ln 0.98\right)^{0.25}\right) \cdot \left( (1,000 - X^*)^{0.3} - 1 \right)
\]
\[
(1,000 - X^*) = \left( \frac{1,000^{0.3} - 1 - \exp\left(-\left(-\ln 0.02\right)^{0.25}\right) \cdot (2,000^{0.3} - 1) + \exp\left(-\left(-\ln 0.98\right)^{0.25}\right)}{\exp\left(-\left(-\ln 0.98\right)^{0.25}\right)} \right)^{\frac{1}{0.3}}
\]
\[
X^* = 1,000 - \left( \frac{1,000^{0.3} - 1 - \exp\left(-\left(-\ln 0.02\right)^{0.25}\right) \cdot (2,000^{0.3} - 1) + \exp\left(-\left(-\ln 0.98\right)^{0.25}\right)}{\exp\left(-\left(-\ln 0.98\right)^{0.25}\right)} \right)^{\frac{1}{0.3}}
\]
\[
X^* \approx -18.23
\]
In this context, negative \(X^*\) values are incoherent and should be rejected.

To save us from further calculations, the table below presents the \(X^*\) values across many combinations of \(\alpha\) and \(\gamma\). Each instance where \(X^*\) is negative is marked as "undef." Here, not only can we see the swaths of incoherent \(X^*\)'s, but we also observe a non-monotonic relationship between \(X^*\) and \(\alpha\). For any column \(\gamma\), going from top to bottom (or bottom to top) we see that \(X^*\) increases and then decreases as \(\alpha\) varies, suggesting inconsistencies in the over- and under-weighting patterns. We also see a curious risk aversion misalignment: For any particular row \(\alpha\), going from left to right, we can see that \(X^*\) starts off slowly decreasing, and then begins rapidly increasing at higher \(\gamma\) levels. This is problematic, as it contradicts the intuitive expectation that for participants with the same level of probability weighting, the participants with the greater risk aversion should be **less** tolerant of loss prospects in the risky option. Also, when we observe the uneven inverted-U shaped relationship between \(X^*\) and \(\alpha\), we see that at higher levels of \(\gamma\), there are unrealistic and **dramatic** jumps in \(X^*\) when transitioning from \(\alpha = 1\) to \(\alpha = 0.95\).

#### (Table 1)
![Image alt](images/Unframed_Prelec_Table.png)
#### (Figure 1)
![Image alt](images/Unframed_Plot.png)

### (b) Dependent Weighting by Complementarity
To rectify the issues arising from independent weighting, we can try a complementary weighting approach. Here, we apply the weighting function to either the probability of gain or the probability of loss and derive the other weighted probability as its complement. Let's try applying the weighting function only to the probability of gain:
$$
w_{gain} = w(p_{gain}), \quad w_{loss} = 1 - w_{gain}
$$
Assuming that \(U(W_{gain}) \neq U(W_{loss})\) and ensuring that \(1 - w_{gain} \neq 0\), our expected weighted utility becomes:
$$
\mathbf{E}[u(W)] = w_{gain} \cdot U(W_{gain}) + (1 - w_{gain}) \cdot U(W_{loss})
$$
In the context of our decision framework, this becomes:
$$
\mathbf{E}[u(W)] = \exp\left(-\left(-\ln 0.02\right)^{\alpha}\right) \cdot 
\frac{(2,000)^{1-\gamma} - 1}{1 - \gamma} + \left(1-\exp\left(-\left(-\ln 0.02\right)^{\alpha}\right)\right)
\cdot \frac{(1,000-X^*)^{1-\gamma} - 1}{1 - \gamma}
$$
This approach seems to address almost **all** of the issues we encountered in the previous strategy:
- **Additivity of Weighted Probabilities:** If \(w_{loss} = 1 - w_{gain}\), we know that \(w_{gain} + w_{loss} = 1\). This ensures a more coherent and consistent probability space.
- **Stable and Well-Defined Solutions:** As can be observed in Table 2, \(X^*\) becomes defined across all relevant parameter values, allowing us to construct questions at higher combinations of \(\alpha\) and \(\gamma\).
- **Consistent and Intuitive Patterns:** Here, the relationship between \(X^*\) and \(\alpha\) tends to be monotonic. For any column \(\gamma\), going from top to bottom, we see that \(X^*\) decreases as \(\alpha\) increases. We also see that for any particular row \(\alpha\), going from left to right, \(X^*\) monotonically decreases. This also aligns with the intuitive expectation that all else equal, more risk-averse individuals should be less tolerant of loss prospects in risky options. We also see much smoother transitions in \(X^*\) as \(\alpha\) varies.
#### (Table 2)
![Image alt](images/Framed_Prelec_Table.png)
#### (Figure 2)
![Image alt](images/Framed_Plot.png)

Now, let us proceed with strategy (b) in constructing our probability weighting quiz. Similar to the risk aversion quiz, we will use adaptive questioning to elicit the participant's probability weighting coefficient. We will also incorporate the participant's risk aversion coefficient &mdash; obtained from the risk aversion quiz &mdash; to tailor the probability weighting questions they are asked. The \(\approx\) 63:37 split in Option B of the risk aversion quiz was deliberately chosen to align with the fixed inflection point at \(1/e\) in our weighting function. This inflection point is where subjective and objective probabilities are always equal. By using this split and making the strong assumption that \(\approx36.79\%\) probabilities are generally accurately perceived, we can make another strong assumption that responses to the risk aversion quiz were not influenced by probability weighting. This allows us to isolate and independently measure both risk aversion and probability weighting.
Let us go through the construction and administration of the probability weighting quiz:

 1. **Initial Question:** Start with some moderate value of \(\alpha\) between 0 and 1. Then, look to the participant's \(\gamma\) to find the indifference loss amount (\(X^*\)). For example, let us start with $\alpha = 0.7$ for a participant with a  \(\gamma\) of 0.9:
    - **Option A:** No bet.
    - **Option B:** A 2\% probability of gaining \$1,000 (Total Wealth: \$2,000) and a 98\% probability of losing \$56.22 (Total Wealth: \$943.78).
    The participant chooses either Option A (the safe option) or Option B (the risky option).
2. **Adaptive Questioning:**
    - **If Option A is chosen,** select a question from a higher \(\alpha\) row (e.g., \(\alpha = 0.75\)).
    - **If Option B is chosen,** select a question from a lower \(\alpha\) row (e.g., \(\alpha = 0.7\)).
 3. **Assigning a Score:** Continue presenting questions, moving up or down the \(\alpha\) scale based on the participant's initial choice. When the participant reverses their choice direction, the quiz concludes and the \(\alpha\) value that aligns the closest with the last choice provides an estimate of the participant's probability weighting coefficient.

# References
**Griffith, R. M.** 1949. "Odds Adjustments by American Horse-Race Bettors." *The American Journal of Psychology* 62, no. 2: 290–294. http://www.jstor.org/stable/1418469.

**Bordalo, Pedro, Nicola Gennaioli, and Andrei Shleifer.** 2012. "Salience Theory of Choice Under Risk." *The Quarterly Journal of Economics* 127, no. 3: 1243–1285. https://doi.org/10.1093/qje/qjs018.