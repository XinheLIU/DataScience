# AB Test

- [AB Test](#ab-test)
  - [Statistics Theory behind A/B Test](#statistics-theory-behind-ab-test)
    - [Hypothesis Testing](#hypothesis-testing)
      - [Type of Tests](#type-of-tests)
      - [alpha (significance)](#alpha-significance)
      - [beta (power)](#beta-power)
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

#### Type of Tests

#### alpha (significance)

#### beta (power)

Errors
  Type II error: False negative
    power = 1-beta
  Type I Error : False Positive
Test
  T-test
  Proportional Test

## A/B Test in practice

### A/B Test Process

#### 1. Set Goals and Assumptions

Good Assumptions

quantificable
can be proven wrong
causal assumptions

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

访问层面和页面层面的单位，比较适合变化不易被用户察觉的 A/B 测试，比如测试算法的改进、不同广告的效果等等；如果变化是容易被用户察觉的，那么建议你选择用户层面的单位。
从用户层面到访问层面再到页面层面，实验单位颗粒度越来越细，相应地可以从中获得更多的样本量。原因也很简单，一个用户可以有多个访问，而一个访问又可以包含多个页面浏览。

保证用户体验的连贯性。
实验单位应与评价指标的单位保持一致。
样本数量要尽可能多。

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
  common control group
  multiple top-line metrics
  segmentation analysis
  check experiments multiple times (p-hacking problem)
solutions
  alpha adjustment
    Bonferroni Correction
  p adjustment : FDR (False Discovery Rate) Control
    Benjamini-Hochberg Procedure

### Learning effect

occurance
  Novelty Effect
  Change Aversion
solutions
  Long-term tests
  Cookie-Cookie-Day(CCD) Test

### SUTVA violation

occurance
  share budget (resource)
  two-side markets
  user-interactions
solutions
  split 
    geomeric
    time
      A/B not simultaneously online (by hour, day, minutes, etc)
    resource/budget
    clustering methods

### Simpson's Paradox

solutions
  balance check
  matching
  rerun

## When A/B Test is not useful

Treatment not controlled
	instrumental variables/proxy varibales

some User Experience problems
	survey / focus group

major event launch

few users

## Reading List / Reference
