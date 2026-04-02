+++
title = '[BBM 5] Limitations & Looking Ahead'
date = '2025-01-04'
math = true
draft = true
+++
#### Levels 2 & 3

# Betting Behavior Methodologies 5: Limitations & Looking Ahead

Hopefully, these write-ups brought to mind a few related ideas and questions that should be explored further. There were also many limitations and several strong assumptions that need further testing and empirical validation. Let's discuss possible next steps.

First, these methods can be used to help model the behaviors around and create strategies for betting on positive expected value bets. That is what the Kelly Criterion was made for, and there already exist a multitude of modified Kelly strategies. One of the most commonly used variants is the "fractional Kelly," which is simply betting a fixed fraction of the standard Kelly fraction (e.g., for "half-Kelly," you bet half of whatever the standard Kelly method prescribes) (MacLean & Thorp 2011). Although the full Kelly Criterion is technically optimal for long-term growth, it makes the strong assumption that the user is fully confident in their edge. As we have observed with probability weighting, even a slight misperception of one's odds can lead to reckless over-betting and **significantly** higher ruin rates. Although fractional Kelly strategies can be effective for managing risk, I would propose testing the Generalized CRRA Kelly Criterion we formulated as a potentially more tailored way of sizing bets according to one's specific risk preferences &mdash; as opposed to choosing some arbitrary fraction. Of course, more empirical testing will be needed to be sure of the usefulness of the Generalized CRRA Kelly Criterion. Also, if we venture into positive expected value bets, the optimal trade-off between maintaining a low rate of ruin and high average final wealth grows less clear, perhaps calling for more attention to the average slopes of log-wealth as a more balanced metric. If we keep the time horizon restricted to a finite number of bets, the dynamic between and independent effects of varying \(\alpha\)'s and \(\gamma\)'s also grow more complex given positive expected value bets.

Aside from probability weighting, there are two other possible theoretical explanations for negative EV betting. First, there is the idea of some additional non-monetary utility component a bettor might receive from the thrill of anticipating a bet's outcome, particularly one that has a large potential payout relative to the bettor's wealth. Before we do any testing, I will propose a simple, preliminary model for this "thrill" utility:
$$
U_{f}(f) = c \cdot \ln(1+sfb)
$$
- **where:**
    - \( c \): the magnitude parameter. It sets the overall scale of how much \( U_{f}(f) \) can contribute relative to monetary utility.
    - \( s \): the sensitivity parameter. It scales how much utility a bettor can derive from some potential gain.

This function has two desirable qualities: (a) it depends on potential gain, and (b) it has diminishing returns. I hypothesize that "potential gains" would likely be a much more powerful incentive for betting than some quality like the exiguity of the win probability itself: although the extreme unlikeliness of a particular winning outcome might provide some thrill after the bet is placed, it likely only serves as a deterrent before the bet is placed. The "thrill" utility's diminishing returns also makes sense: going from, say, doubling the bankroll potential to tripling it likely does not feel proportionally as exciting as the first incremental increase in potential gain. Incorporating this into the overall framework would look something like:

$$
\textbf{E}[U_{\text{total}}(W, f)] = p \cdot U_m(W(1+fb)) + (1-p)\cdot U_m(W(1-f))+U_f(f)
$$

- **where:**
    - \( U_m(\cdot) \): the monetary utility (e.g., CRRA, logarithmic, etc.).
    - \( U_f(f) \): the "thrill" utility as described above.

If the bet is negative EV from a purely monetary standpoint, a rational bettor should, in principle, choose \( f=0 \). Now, with the added utility of \( U_f \), a small \( f>0 \) might yield a higher **total** utility than not betting, despite the negative EV. This would model how the "thrill" of getting to anticipate potential gains might compensate for the monetary shortfalls. Like with probability weighting-induced negative EV betting, the bettor is still risk-averse in the monetary sense: If offered an alternative bet with the same \( U_f \), the bettor should still prefer the one with the higher expected value or lower risk

Another alternative is the idea of a "target wealth:" a bettor walks into a casino with a desired final wealth in mind, and expects to receive some extra satisfaction (some "bonus" utility) if they hit their goal. If they walk in with \$1,000 with the ambition of doubling their wealth, they may reach \$1,999 &mdash; an already fortunate outcome given negative EV bets &mdash; and still feel dissatisfied, or at least willing to place a few more bets because of how close they are to their initial goal. It might also make sense for returns in excess of the bettor's goal to yield diminishing returns, and thus the bonus utility, \( B(\cdot) \), should be some concave function of the wealth, \( W \), in excess of the target, \( \textbf{T} \). We can define the excess wealth as \( \Delta = W - \textbf{T} \) and \( B(\Delta) \) as:

$$
    B(\Delta) = \begin{cases}
                    0 & \text{if } \Delta < 0\\
                    c \cdot \ln(1+s\Delta) & \text{if } \Delta \geq 0. 
                \end{cases}
$$

- **where:**
    - \( c \): the magnitude parameter
    - \( s \): the sensitivity parameter

The expected utility of placing a bet would then look like:
$$
\textbf{E}[U_{\text{total}}(f)] = p \cdot U_{\text{total}}(W_{\text{win}})+(1-p)\cdot U_{\text{total}}(W_{\text{lose}})
$$
For practical implementation, if we consider a case where \( B(W) = c \cdot \ln(1+s \cdot \max(0, W-T)) \), then expected utility can be written as:
$$
\textbf{E}[U_{\text{total}}(f)] = p \cdot (U(W_{\text{win}}) + B(W_{\text{win}})) + (1-p) \cdot U(W_{\text{lose}}) + B(W_{\text{lose}})).
$$
This concept also calls into question the idea that more conservative bet sizing approaches are always better for negative EV bets. As observed in the simulations we ran, although more aggressive strategies performed worse by the end, they also often experienced higher peak wealth levels. If a bettor prioritizes reaching a certain target wealth over maximizing long-term wealth, conservative betting &mdash; or betting in a way that focuses on **minimizing losses** &mdash; might virtually eliminate the possibility of attaining their goal, whereas aggressive strategies with higher ruin rates might at least provide some nonzero probability that they can hit their target. The point at which they hit their target wealth might also work as a more sensible termination point than the arbitrarily chosen ceiling of \( T \) bets.

Let us also discuss several of the limitations of our methodologies we encountered. Most of our methods operate on the premise that individual preferences conform to a CRRA model. While CRRA is elegant and has many intuitive features &mdash; such as the diminishing marginal utility of wealth &mdash; it is certainly not universally applicable. In practice, individuals can very plausibly exhibit increasing or mixed forms of risk aversion not captured by CRRA. By excluding alternative frameworks, such as the cumulative prospect theory value function or some non-constant relative risk aversion model, we are relying on a very specific view of risk-taking (Tversky & Kahneman 1992). The design of our CRRA quiz deliberately avoids the domain of losses by presenting options entirely composed of gain prospects, sidestepping the exploration of concepts such as loss aversion and risk-seeking behavior in losses. This narrow focus on gains may not necessarily reflect how individuals approach bets involving the risk of losing part of their principal wealth. The assumption that the quiz is equally valid without reference to losses or more complex payoff structures is untested and, in practice, may also limit how deeply participants engage with the questions.

Our adaptation of the probability weighting function independent of adjacent prospect theory concepts may also raise concerns. By isolating probability weighting from the effects described by loss aversion and the value function, we are capturing only one dimension of behavioral biases, inevitably simplifying the ways individuals actually evaluate risky prospects in "irrational" ways. Moreover, our application of a dependent weighting-by-complementarity strategy may be limited when individuals can use different weighting schemes for gains versus losses. How much someone might overweight an unlikely gain prospect (e.g., overweight their willingness to pay for a lottery ticket) is not necessarily reflective of their tendency to overweight an unlikely gain prospect (e.g., overweight their willingness to pay for insurance). Our model's reliance on a single function and a single parameter, \( \alpha \), presumes uniform distortion across different probability ranges for gains, ignoring potentially different patterns at the extremes or for losses.

The \( \approx \) 63:37 split used in our CRRA function to isolate measures of risk aversion and probability weighting rest on the Prelec function's inflection point at \( 1/e \). While this is a clean, well-known formulation, it is based on empirical generalizations placing the "neither overweighted nor underweighted" probability between roughly 0.3 and 0.4 (Prelec 1998).  The assumption that everyone perceives probabilities of \( \approx 36.79\% \) is a strong oversimplification, as real individuals could have very different thresholds. In fact, one could argue that due to people's frequent exposure to coin flip scenarios and often misinformed applications of the principle of indifference, 50\% might serve as a more intuitive inflection point (Bruin & Carman 2012). Regardless of where it should be placed, we can always move the inflection point by using the two-parameter form of Prelec's weighting function:
$$
w(p) = \exp\left(-\beta(-\ln p)^\alpha\right)
$$
- **where:**
    - \( \beta \): a multiplier on \( \left(-\ln p\right)^\alpha \) that shifts the function vertically along the probability axis.

To move the fixed location of the inflection point, we can simply set the weighted function of the desired point equal to the objective probability, solve for \( \beta \), and plug that back into the two-parameter form. For example, if we found empirical evidence that \( 50 \% \) probabilities are generally the most accurately perceived, we could derive an alternate form as follows:
$$
w(0.5) = \exp\left(-\beta\left(-\ln\left(0.5\right)\right)^{\alpha}\right) = 0.5
$$
$$
\ln\left(\exp\left(-\beta\left(\ln 2\right)^{\alpha}\right)\right) = \ln(0.5)
$$
$$
-\beta\left(\ln 2\right)^{\alpha} = \ln(0.5)
$$
$$
-\beta\left(\ln 2\right)^{\alpha} = \ln(0.5) \\
\quad \Rightarrow \quad \beta = -\frac{\ln(0.5)}{\left(\ln 2\right)^{\alpha}}
$$
$$
\beta = -\frac{-\ln(2)}{\left(\ln 2\right)^{\alpha}} = \frac{\ln(2)}{\left(\ln 2\right)^{\alpha}} = \left(\ln 2\right)^{1 - \alpha}
$$
- **Substituting back into \( w(p) \)**...
$$
w(p) = \exp\left(-\left(\ln 2\right)^{1 - \alpha} \cdot \left(-\ln p\right)^{\alpha}\right)
$$
Make note that such alternate forms may lose certain qualities of the standard form, such as compound invariance. Setting the fixed inflection point to \( 50\% \) also does not make the function symmetric about 0.5; it will still run into the non-additivity issues (\( w_{\text{gain}} + w_{\text{loss}} \neq 1 \) when independently weighting both probabilities) we encountered with the standard form.

The actual designs of the risk aversion and probability weighting quizzes adopt many simplifying choices that may significantly shape participants' responses. The choice of \$1,000 as a baseline wealth is arbitrary; participants asked to "imagine" they have exactly this amount might not relate accurately if their actual wealth or mental reference levels differ. Similarly, the particular payoffs, probabilities, and question formats (e.g., listing a certain gain vs. a risky gain) reflect a framing that could influence how seriously or realistically participants react. Minor changes, such as starting with \$2,000 or adjusting the safe gain from \$150 to \$200 can elicit varying responses from different participants. Furthermore, the manner of quiz administration (in-person, online, time-limited, etc.) can trigger widely varying reactions. We have yet to establish a single standardized protocol to control for framing effects (Yang & Vosgerau 2013).

Also, our focus has only been on a few stylized bet types &mdash; just binary bets with known probabilities and payoffs &mdash; rather than many of the more complex games that can be found in real casinos or financial markets. Although this simplification facilitates mathematical traceability, it excludes perhaps important complexities such as incomplete information, strategic interaction with other players, or dynamically updating probabilities. Extending the approach to multi-agent games like poker or to dynamic betting in sports markets would likely necessitate incorporating game-theoretic solutions, more elaborate state representations, and/or evolving beliefs. Our current assumptions (e.g., stable, known probabilities) do not necessarily translate to these contexts, where partial information and strategic behavior can significantly shape outcomes.

Furthermore, there may exist some disconnect between our "Generalized CRRA Kelly" formula &mdash; a systematic way to compute bet fractions given varying risk-aversion levels &mdash; and how real bettors with varying risk-aversion levels actually behave. There is no guarantee that real bettors actually optimize their bets at each step according to such a solution, and we have yet to empirically test how closely CRRA Kelly bet sizing actually aligns with intuitive human betting behavior. Human bettors may succumb to time inconsistency, emotional swings, or other misunderstandings of odds. Thus, for now, the simulation is best viewed as an internally consistent theoretical framework, rather than a fully validated model of actual behavior. Additionally, the simulation halts after a fixed number of rounds (e.g., 10,000), an arbitrary but necessary condition to avoid indefinite loops. It is untested that bettors actually approach betting decisions in repeated identical trials up to a large maximum, and different stopping rules may generate different observed outcomes.

# References

**MacLean, Leonard C., Edward O. Thorp, and William T. Ziemba.** 2011. *The Kelly Capital Growth Investment Criterion*. WORLD SCIENTIFIC. https://www.worldscientific.com/doi/abs/10.1142/7598.

**Prelec, Drazen.** 1998. "The Probability Weighting Function." *Econometrica* 66(3): 497–527. http://www.jstor.org/stable/2998573.

**Bruine de Bruin, Wändi, and Katherine G. Carman.** 2012. "Measuring Risk Perceptions: What Does the Excessive Use of 50% Mean?" *Medical Decision Making* 32(2): 232-236. https://doi.org/10.1177/0272989X11404077.

**Yang, Yang, and Joachim Vosgerau.** 2013. "Framing Influences Willingness to Pay but Not Willingness to Accept." *Journal of Marketing Research* 50: 725-738. https://doi.org/10.1509/jmr.12.0430.

**Tversky, Amos, and Daniel Kahneman.** 1992. "Advances in Prospect Theory: Cumulative Representation of Uncertainty." *Journal of Risk and Uncertainty* 5(4): 297-323. http://ideas.repec.org/a/kap/jrisku/v5y1992i4p297-323.html.
