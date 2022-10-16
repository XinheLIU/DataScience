# AB Test

- [AB Test](#ab-test)
  - [Statistics Theory behind A/B Test](#statistics-theory-behind-ab-test)
    - [Hypothesis Testing](#hypothesis-testing)
      - [Type of Tests](#type-of-tests)
  - [A/B Test in practice](#ab-test-in-practice)
    - [A/B Test Process](#ab-test-process)
      - [1. Set Goals and Assumptions](#1-set-goals-and-assumptions)
      - [2. Define metrics](#2-define-metrics)
      - [3. Determine experiment units](#3-determine-experiment-units)
      - [4. Estimate sample size & Power](#4-estimate-sample-size--power)
      - [5. split experiment groups](#5-split-experiment-groups)
    - [6. Determine Observation cycle](#6-determine-observation-cycle)
      - [7. experiment](#7-experiment)
      - [8. Analyze results](#8-analyze-results)
  - [Challenges in A/B Test](#challenges-in-ab-test)
    - [Multiple testing problem](#multiple-testing-problem)
    - [Learning effect](#learning-effect)
    - [SUTVA violation](#sutva-violation)
    - [Simpson's Paradox](#simpsons-paradox)
  - [When A/B Test is not useful](#when-ab-test-is-not-useful)
  - [Reading List / Reference](#reading-list--reference)

## Statistics Theory behind A/B Test

### Hypothesis Testing

Statistical Test Details

- Type I Error : False Positive
  - Significance ($\alpha$)
- Type II error: False negative
  - Power ($1-\beta$)

#### Type of Tests

- T-test
- Proportional Test

## A/B Test in practice

### A/B Test Process

#### 1. Set Goals and Assumptions

Good Assumptions

- quantificable
- can be proven wrong
- causal assumptions

#### 2. Define metrics

How to find good metrics

- Product + Life Cycle Stage of the Product
- Better Quantifiable, sometimes qualitative metrics also

Metrics needs to be determined

- Evaluation Metrics
- Guardrail Metrics: use for Sanity Check
  - A/B test is inline with long-term goals
  - experiment set up is fine
- OEC(overall-evalutation-criteria)

#### 3. Determine experiment units

Choose Units based on

- visit (request) level, page level: changes not explicitly perceivable by users (eg. algo change, ads change)
  - advantage: more sample, high power
  - disadvantage: users in different groups
- user level: user explicitly perceive
  - ensure user experience persistency
- split units should be same as evaluation metric calculation units(ideally)

Units must satisfy

- SUTVA(stable-unit-treatment-value)
  - positivity
  - i.i.d assumption: The potential outcomes for any unit do not vary with the treatments assigned to other units
  - Treatment Consistency

Check split balance
  
- sample size
- feature distribution(can be guardrail metrics)
  - simpson's paradox
  - Matching methods

#### 4. Estimate sample size & Power

#### 5. split experiment groups

randominization methods

### 6. Determine Observation cycle

p-hacking problem

#### 7. experiment

#### 8. Analyze results

Bootstrapping

## Challenges in A/B Test

### Multiple testing problem

occurance

- common control group
- multiple top-line metrics
- segmentation analysis
- check experiments multiple times (p-hacking problem)

solutions

- alpha adjustment
  - Bonferroni Correction
- p adjustment : FDR (False Discovery Rate) Control
  - Benjamini-Hochberg Procedure

### Learning effect

occurance

- Novelty Effect
- Change Aversion

solutions

- Long-term tests
- Cookie-Cookie-Day(CCD) Test

### SUTVA violation

occurance

- share budget (resource)
- two-side markets
- user-interactions

solutions

- split
  - geomeric
  - time
    - A/B not simultaneously online (by hour, day, minutes, etc)
  - resource/budget
  - clustering methods

### Simpson's Paradox

solutions

- balance check
- matching
- rerun

## When A/B Test is not useful

- Treatment not controlled
  - instrumental variables/proxy varibales
- some User Experience problems
  - survey / focus group
- major event launch
  - few users

## Reading List / Reference