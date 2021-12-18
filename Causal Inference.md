# Causal Inference

## Key Concepts

- Causality
  - Association vs Causation
    - Reverse Causation
    - Selection Bias
      - [Berkson's Paradox](https://en.wikipedia.org/wiki/Berkson%27s_paradox)
    - Confounding Bias
      - [Simpson's Paradox](https://en.wikipedia.org/wiki/Simpson%27s_paradox)
  - The Ladder of Causality
    - Association
    - Intervention
    - Counter-factual
- Methods to Test Causality
  - Randomized Controlled Experiments
  - Observational Study （eg. natrual experiments)
    - Source of Errors
      - Random Error: reduced by [Law of Large Numbers](https://en.wikipedia.org/wiki/Law_of_large_numbers)
      - System Error
        - Instrumental: Causal Models selection,etc
        - Methods Errors: sampling bias
      - Gross Error: educed by Cross Validation, Tests, reversed experiments
    - Methods to Reduce The Effects of Confounding
      - confounders known
        - Matching
          - low-dimension
            - CEM
          - high-dimension
            - PSM (common support assumptions)
            - [distance measures](https://en.wikipedia.org/wiki/Statistical_distance)
          - models
            - KNN, kernel density, radis, hierarchical
            - relies on sampling methods & parameter selection
        - Weighting
          - IPW, IPTW
          - stratification
        - regression adjustment
          - $$q(x,t) = E(Y|X, T)$$
      - confounders unkown
        - has time-series stability
          - Did(Difference in Difference)
          - CUPED
        - [Synthetic Control Methods](https://en.wikipedia.org/wiki/Synthetic_control_method)
          - $$min(X_1 - X_0 w) ^ T V (X_1 - X_0w)$$
      - Control Special Treatments
        - backdoor & frontdoor variables
        - IV (Instrumental Variables)
        - Double negative controls
- Causal Models
  - RCM: Potential Outcome Framework(Rubin Causal Model)
    - Assumptions
      - SUTVA(Stable Treatment Value Assumptions)
      - [Unconfoundeness](https://www.degruyter.com/document/doi/10.1515/jci-2013-0011/html)
      - Positivity: any unit has positive probability to be treated by x
    - Basic Concepts
      - Unit
      - Treatment, Outcome, Potential Outcome
      - ATE, ATT, ATC(average treatment); CATE(conditional ATE); HTE
      - ITE(Individual Treatment Effect)
    - Methods
      - confounders: use Methods to Reduce The Effects of Confounding
      - [ITE](https://arxiv.org/abs/2108.04939) (HTE) estimatin
        - Meta Learners
        - Generalized Random Forest
          - can handle lower dimension confounders
          - overfitting
        - DML (Double Machine Learning)
        - Orthogonal Random Forest
- Structural Causal Model (SCM) (Pearl)
  - Graphical Models
    - Building blocks
      - Chain
        - Mediator
        - A ind C | B
    - Fork
      - Confounder
        - A ind C | B
    - V-structure immorality
      - Collider
      - A not ind C | B
    - do operator
    - backdoor criterion
    - frontdoor criterion
    - Common Methods
      - Instrumental Variable
      - Backdoor Criteria
      - Frontdoor Criteria
      - Double Negative Control

## Reading List

Causal Inference

- The Book of Why
- Causal Inference in Statistics

Randomized Controlled Experiments

Observational Studies

## Case Studies
