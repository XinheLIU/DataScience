# Causal Inference Learning List

- [Causal Inference Learning List](#causal-inference-learning-list)
  - [Consal Inference Key Concepts](#consal-inference-key-concepts)
    - [Causality != correlation (causation != association)](#causality--correlation-causation--association)
    - [What is Causality](#what-is-causality)
    - [How to measure Causality](#how-to-measure-causality)
      - [A/B Test (RCT, randomized controlled trials)](#ab-test-rct-randomized-controlled-trials)
      - [Observational Study](#observational-study)
        - [1. Problem \& Assumptions formulation](#1-problem--assumptions-formulation)
        - [2. Meature cusal effects using observational Data](#2-meature-cusal-effects-using-observational-data)
        - [3. Learn by data](#3-learn-by-data)
  - [Reading List](#reading-list)

## Consal Inference Key Concepts

### Causality != correlation (causation != association)

1. reverse causality
    1. bugs/dislike feedback vs user activeness
2. Prediction vs Intervention
   1. customer churn problem: prediction might not be effective
      1. Retention Futility: Targeting High-Risk Customers Might be Ineffective
      2. 地心说 ：Data Generation Process (DGP) is unkown
3. "Biases" in data
   1. Confonding Bias (common cause)
      1. Ads click rate vs user retention: usually positively correlated -> doesn't mean improving ads click can improve retention
      2. Game users converted into other game ads have lower retention -> doesn't mean no ads for them
4. Selection Bias (conditioning on common effects)
   1. [Berkson's Paradox](https://en.wikipedia.org/wiki/Berkson%27s_paradox) : resume qualification vs effectivensss
      1. Ads bidding price & conversion rate usually negatively correlated
   2. [Yule-simpson paradox](https://en.wikipedia.org/wiki/Simpson%27s_paradox)

### What is Causality

- No universal definition, usually about "conterfactual problem" or "potential outcome
- The Ladder of Causality
  - Association
  - Intervention
  - Counter-factual

### How to measure Causality

#### A/B Test (RCT, randomized controlled trials)

- Assumptions: SUITVA (stable unit treatment value assmption)
   1. No interference: potential outcome only varies by treatment
   2. Consistency : no different versions of treatment

#### Observational Study

##### 1. Problem & Assumptions formulation  

> set target

1. Estimand : quantity to be estimated
2. Estimate: approximation of estimand using finite data
3. Estimator: method or formula for estimate

##### 2. Meature cusal effects using observational Data

> get empirical estimands

Indenfication/[Identifiablity](https://en.wikipedia.org/wiki/Identifiability)

- A model is identifiable if it is theoretically possible to learn the true values of this model's underlying parameters after obtaining an infinite number of observations from it. Mathematically, this is equivalent to saying that different values of the parameters must generate different probability distributions of the observable variables.
  
Potential Outcome Framework (Neyman-Rubin Causal Model) (POM)

 1. Effect definition
    1. ATE(Average Treatment Effect), ATT (Average Treatment on the Treated), CATE(Conditional Average Treatment Effect), HTE(Heterogeneous Treatment Effec), ITE(Individual Treatment Effect) , Intent-to-Treat, Local ATE
 2. Assumptions
    1. SUITVA (stable unit treatment value assmption)
       1. No interference: potential outcome only varies by treatment
       2. Consistency : no different versions of treatment
 3. Under what conditions ATE is identifiable
    1. Unconfoundedness/ ignorability/ Conditional Independence Assumption (CIA) / Exogeneity : no unmeasured confounders, given confounders' values, Treatment is independent from Potential Outcome
    2. Positivity/Common Support: each unit have positive probailit to be trated

Structural Causal Models/ DAG (Directed Acyclic Graphs) (SCM)

- Relationship definition
   1. Cahins (mediators) : X-> Z-> Y, Forks (confounders) X<-Z->Y, Colliders: X->Z<-Y
   2. d-separation
- Do calculus
  - Do operator (intervention)
  - Backdoor adjustment
  - Front Door adjustment

##### 3. Learn by data

> get estimation strategies

Causal Inference Tools

1. Regression/Machine Learning Models
   1. Assumptions: Exogeneity (residual not correlated with X, no backdoor), other assumptions mainly inflence variance
2. Matching (matching is weighting with 0 weights)
   1. Assumptions: CIA, positivity, Balance Check(after matching, marginal distribution on confounders the same)
   2. Exact Matching, Coarsened Exact Matching(CEM)
      1. Mahalanobis Distance Matching (has course of dimensionality)
      2. [distance measures](https://en.wikipedia.org/wiki/Statistical_distance)
   3. Propensity Score Mathing (PSM)
      1. Propensity score = p(T=1|X)
3. Weighting(/Weighting)
   1. Inverse Probaility Weighting/Inverse Propensity Score Wighting (IPTW): weight with 1/propensity score
4. Instrumental Variables(IV)
   1. Assumptions:
      1. relevance of the instrument (Cov(Z,X) large to ensure low variance)
      2. Validity of the Instrument/Exclustion restriction: Z can only affect Y by X
      3. Monotonicity: Z affects X monotioncally ("transivity")
   2. Estimate : Cov(Z,Y)/Cov(Z,X)
   3. Limitation: Can only estimate LATE(local average treatment effect/compiler average causal effect, CACE)
5. Regression discontinuity
   1. Assumtion: same distribution around cut off
   2. Limitatin: bandwith needs to be determined, only estimates the effect around cutoff point
6. Difference-in-Difference (DID)
    1. Assumption: Parallel Trends Assumptions (very sensitive to metric transformation)
7. [Synthetic Control](https://en.wikipedia.org/wiki/Synthetic_control_method)
   1. Assumptions: basically Did combined with Matching (same assmptions) : balanced pre-treatment
   2. Estimates: $$min(X_1 - X_0 w) ^ T V (X_1 - X_0w)$$
   3. Limitations: Needs relatively long pre-treatment data

Sensitivity Analysis

> Causal assumptions sometimes are intestable, use robustness tests for valid results, common test methods

- Add random coomon cause
- placebo treament
- dummy outcome
- simulated outcome
- add unobserved common causes
- data subsets validation
- Booststrap validation

## Reading List

Causal Inference

- Causal Inference in Statistics: A Primer, Pearl, Glymour, Jewell
- The Book of Why: The New Science of Cause and Effect, Pearl
- Causal Inference in Statistics
- Counterfactuals and Causal Inference: Methods and Principles for Social Research, Morgan, Winship
- Elements of Causal Inference: Foundations and Learning Algorithms, Peters, Janzing, Schoelkopf

Free Online Books/Resources

- [Causal Reasoning: Fundamentals and Machine Learning Applications](https://causalinference.gitlab.io/book/)
- [The Effect: An Introduction to Research Design and Causality](https://theeffectbook.net/)
- [Causal Inference: The Mixtape](https://mixtape.scunning.com/introduction.html)
- [Causal Diagrams: Draw Your Assumptions Before Your Conclusions](https://www.edx.org/course/causal-diagrams-draw-your-assumptions-before-your)
- [Introduction to Causal Inference](https://www.bradyneal.com/causal-inference-course), Brady Neal
- [Applied Causal Analysis (with R)](https://bookdown.org/paul/applied-causal-analysis/)
- [Lecture Notes for Causality in Machine Learning](https://bookdown.org/robertness/causalml/docs/)

Randomized Controlled Experiments

Observational Studies

Mastering Metrics: The Path from Cause to Effect, Angrist, Pischke
Design of Observational Studies, Rosenbaum