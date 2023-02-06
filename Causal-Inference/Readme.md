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
  - [Causal Machine Learning / Uplift Models](#causal-machine-learning--uplift-models)
    - [CIA Assumption satisfied](#cia-assumption-satisfied)
      - [Meta-Learners](#meta-learners)
      - [Doubly Robust Learners (DRL)](#doubly-robust-learners-drl)
      - [Double Machine Learning (DML)](#double-machine-learning-dml)
      - [Tree-based Models (Causal Tree/Forest)](#tree-based-models-causal-treeforest)
    - [CIA Assumption not satistifed](#cia-assumption-not-satistifed)
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
    2. No interference: potential outcome only varies by treatment
    3. Consistency : no different versions of treatment
 3. Under what conditions **ATE is identifiable**
    1. Unconfoundedness/ ignorability/ **Conditional Independence Assumption (CIA)** / Exogeneity
       1. no unmeasured confounders, given confounders' values, Treatment is independent from Potential Outcome
    2. Positivity/Common Support/Overlap: each unit have positive probailit to be trated

Structural Causal Models/ DAG (Directed Acyclic Graphs) (SCM)

- Relationship definition
   1. Cahins (mediators) : X-> Z-> Y, Forks (confounders) X<-Z->Y, Colliders: X->Z<-Y
   2. d-separation
- do calculus
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

## Causal Machine Learning / Uplift Models

> Application of Causal Models

Causal Machine Learning/Uplift Models are just Machine Learning Models to learn Causal Relationships (Heterogenous treatment effects, HTEs) from experimental/observational data. It could be thought as traditional machine learning algorithms with structure constraints imposed (search in a smaller functional space). While most ML algorithms are good with prediction, it needs to follow Causal Inference assumptions/frameworks to learn proper causal relationships.

Application in Ads/Recommender System

- [EconML](https://econml.azurewebsites.net/spec/motivation.html)
- Ads Delivery: ROI maximization (Cost minimization) under constraint of Daily New Users (DNU, or LT/LTV, Life Time/Life Time Value)
- Inventive/Bonus Program: maximize commercial value (LTV) under the constraint of user stay time (Life Time)
- Ads Strategy: Customize Ad Load/Ad Gap, maximize commercial value (Advertiser's value), minimize user experience loss(Stay time, Life Time, etc)

### CIA Assumption satisfied

As mentioned in POM Framework, Learn Causal Relationship from observational data needs to satisfy

- SUIVA
- CIA (or unconfoundedness under SCM framework)
- postivity/overlap

assumptions. We can inference

$$E(Y|X=x, T=t) = E(\sum I(T=t') Y(t') | X=x, T=t] (SUITA)$$
$$=E(\sum I(T=t') Y(t') | X=x) (CIA + positivity) $$
$$=E(Y(t)|X=x)$$

#### [Meta-Learners](https://arxiv.org/abs/1706.03461)

- Pros:
  - robust, can choose ML models at different state
- Con
  - may lose inference properties (confidence interval, asympototic normality)

[S-Learner](https://econml.azurewebsites.net/spec/estimation/metalearners.html#s-learner)

- $$\hat{\tau(x)} = E[Y(1) | x, T=1 ] -  E[Y(0) | x, T=0 ] = \hat{mu(x,1)} - \hat{mu_0(x, 0)}$$
- Pros: simple, applies to sample size large or high singal-noise-ratio (SNR) scenario
- Cons low sample utilization, has regularization bias

[T-Learner](https://econml.azurewebsites.net/spec/estimation/metalearners.html#t-learner)

- $$\hat{\tau(x)} = E[Y(1) | x ] -  E[Y(0) | x ] = \hat{mu_1(x)} - \hat{mu_0(x)}$$
- Pros: simple, applies to sample size large or high singal-noise-ratio (SNR) scenario
- Cons low sample utilization, has regularization bias, when X is high-dimensional, T's effect is hard to learn (highly biased, can be debiased by DRL)

[X-Learner](https://econml.azurewebsites.net/spec/estimation/metalearners.html#s-learner)

- estimates CATT(CATE on treated) and CATC (CATE on control) then take weighted average (by propensity score)
- [Domain Adaptiation Learner](https://econml.azurewebsites.net/spec/estimation/metalearners.html#domain-adaptation-learner)
- Tarnet

#### Doubly Robust Learners (DRL)

> [Formulation](https://econml.azurewebsites.net/spec/estimation/dr.html)

Two tasks
- predict Y based on confounders (X and W, X has fixed dimensions, W's dimension can increase with more samples)
- predicted propensity score based on X, W
- Categorical Treatments

$$Y(t) = g_t(X, W) + \epsilon_t, E(\epsilon_t |X, W) = 0$$ (T-Learner)
$$Pr(T=t |X, W) = p_t(X, W)$$
$$\{Y(t)\}_{t=1}^{n_t} \perp T | X, W$$
result:
$$Y(t)_i^{DR} = g_t(X,W) + \frac{Y_i - g_t(X_i, W_i)}{p_t(X_i, W_i)}$$
$$HTE = Y(1)_i^{DR} - Y(0)_i^{DR}$$

- Pros
  - "Robust" in a sense that one of two tasks is correct, estimation is correct (Debias to give more weights to unexpected sample results)
  - improved sample utilization
- Cons
  - two models, hard to implment End-to-End

End-to-End example

- Dragonnet

#### Double Machine Learning (DML)

Two tasks

- Predict Y based on X and W, only train on untreated data (control group)
- predict T based on X, W

$$Y(t) = \theta(X) \cdot T  + g(X, W) + \epsilon, E(\epsilon |X, W) = 0$$ (T-Learner)
$$T = f(X, W) + \eta, E(\eta |X, W) = 0, E(\epsilon \cdot \eta |X, W) = 0 $$
$\theta(X)$ is the treatment effect. To estimate it,
$$Y(t) - E(Y | X, W)= \theta(X) \cdot (T - E(T | X, W)) + \epsilon$$ (substract expecation of Y)

Build 2 Machine Learning Models

- $$q(X, W) = E(Y | X, W)$$
- $$f(X, W) = E(T | X, W)$$

residuals of the two models

- $$\tilde{Y} = Y- q(X, W)$$
- $$\tilde{T} = T - q(X, W)$$

then

$$\tilde{Y} = \theta(X) \cdot  \tilde{T}+ \epsilon$$

regress to get effect
$$\theta(X) = argmin E_n[Loss(\tilde{Y} - \theta(X) \cdot \tilde{T})]$$

Pros and Cons

- can learn both discrete and continuous treatments
- suitable for high-dimensional data
- good inference property (when Neyman Orthogonality and corss fitting satistfied)
- Suitable for tree-based models, LATE

#### Tree-based Models (Causal Tree/Forest)

> [EconML Link](https://econml.azurewebsites.net/spec/estimation/forest.html)

Use DML Framework with Generalized Random Forest (Link)

- Estimate LATE (Local likelihood), not global likelihood
- Interpretable
- Inference properties 

Cons 

- Binary Treatment




### CIA Assumption not satistifed





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