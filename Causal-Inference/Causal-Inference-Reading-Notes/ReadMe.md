# Notes for Learning the Pumpkin-Book Project

> The [Pumpkin Book Project](https://github.com/datawhalechina/pumpkin-book) is ...

- [Notes for Learning the Pumpkin-Book Project](#notes-for-learning-the-pumpkin-book-project)
  - [Chpater 1 Introduction](#chpater-1-introduction)
  - [Chapter 2 Model Evaluation](#chapter-2-model-evaluation)
  - [Chapter 3 Linear Regression](#chapter-3-linear-regression)
  - [Chapter 4 Decision Tree](#chapter-4-decision-tree)
  - [Chapter 5 Neural Networks](#chapter-5-neural-networks)
  - [Chapter 6 SVM](#chapter-6-svm)
  - [Chapter 7 Bayesian Classifier](#chapter-7-bayesian-classifier)


## Chpater 1 Introduction

Key Concepts

- Machine Learning
  - Mitchell 1997
  - learning algorithm : generate a model based on (empirical) data
- generalization
  - training, validation
- tasks
  - supervised learning, unsupervised learning, clustering etc

Homework

1. No-free Lunch Theorem (Wolpert, 1996; Wolpert and Macready 1995)
   1. 练习1.4 1.5
2. 整理李沐Chapter1 Notes


## Chapter 2 Model Evaluation

Key Concepts

1. overfitting
2. cross-validation methods
   1. leave-one-out (LOO)
   2. K-fold
   3. Bootstraping
3. precision, recall, confusion matrix
   1. P-R Graph
   2. ROC and AUC
4. Hypotesis Test (on 2 learners)
   1. Binomial Test
   2. t-test
   3. McNemar Test
   4. Friedman & Nemenyi Test

Homework

1. 推导2.22 AUC vs l_rank
   1. https://tracholar.github.io/machine-learning/2018/01/26/auc.html
   2. 拓展阅读[AAUC UAUC](https://bytedance.feishu.cn/docs/doccnnnDYy5MMMhCgw39Y7V5CGg)
2. 推导2.41 Bias-Variance Tradeoff
   1. ![](2023-01-12-09-18-53.png)
3. 拓展阅读 常见的统计检验（整理到：统计学）
   1. 二项检验等
   2. All of Statistics + 之前的课件（Columbia + CMU 复习）
4. Confusion Matrix vs 1-2类错误率 （阐述+概述+沉淀）
5. Cross-validation code practice
   1. 参考 Datawhale公众号

## Chapter 3 Linear Regression

Concepts

- Linear Regression
- Logistic Regression
- LDA
  - Generalized Rayleigh quotient
- Gradient Descent, Newton's Method
- multi-class classification problem
  - MvM (many-vs-mang), OVO(one-vs-one), OVR(one-vs-the rest)
- class imblanace / sample imbalance problem

Homework

1. 线性回归
   1. 手推 rss rse （all of statiatics） 公式3.5-3.7
   2. 单变量导数 解析解 （isl）
2. 线性回归
   1. matrix cookbook 矩阵求导 大致讲清楚 （3.10-3.10）（绿书+Matrix cookbook + 俄罗斯课件+知乎）
   2. 手推matrix解法 （绿书 esl）公式3.9-3.12
3. 数学基础
   1. hessian矩阵（quant面试书 说明干啥用） 泰勒公式
   2. 梯度下降法 牛顿法（复习mscf math）
   3. 拉格朗日函数 Optimization （百科）（凸优化找参考书）
4. logistic
   1. 解释1: 用wx + b 逼近odds （logit）
   2. 一阶导数 二阶导数的gradient（手写+ python实现 李沐 + 手推机器学习参考）（3.27-3.30）
5. LDA
   1. 解释1 协方差解释 lda 求导（先看懂, 再结合看isl说明， 复习CMU相关课件）（3.39-3.45）
6. Coding Practice
   1. Linear regression in Py 所有包
   2. Logistic regression in py
   3. LDA in Python (read doc)
7. Coding 类别不平衡问题 sklearn 实现 smote 实现 说明的代码（一些说明的文字）


下载书

- [1] Wikipedia contributors. Matrix calculus, 2022.
- [2] 张贤达. 矩阵分析与应用. 第 2 版. 清华大学出版社, 2013. [3] 王燕军. 最优化基础理论与方法. 复旦大学出版社, 2011.

## Chapter 4 Decision Tree

Concepts

1. Information Entropy, Information Gain, Gini Index
2. Decision Tree Algorithms
   1. ID3 - Interative Dichotomiser (Quinlan 1986) uses Info Gain
   2. C4.5 (Qinlan 1993) uses Info Gain Ratio
   3. CART (Briedman et al 1984, Murthy 1998) uses Gini Index
3. Pruning, pre-pruning, post-pruning


Homework

1. 推导Entropy 最大值（4.1）
2. 拓展阅读 Causal Tree (Generalized Decision Tree), Causal Forest Paper & Code
3. Coding 
   1. Decision tree in Python (how to choose ID3, C4,5, CART). in Xgboost? how did they handle missing values?
4. 拓展阅读 Multivariate decision-tree
   1. OC1 ( Murthy et al 1994, Broadly and Utgoff 1995)

## Chapter 5 Neural Networks

Concepts

1. MLP (multi-layer Perceptron)
   1. hidden-layer
2. BackPropagation(BP)
   1. gradient descent of sigmoid function $f'(x) = f(x)(1-f(x))$
3. Heuristic Optimization Algorithms
   1. simulated annealing
   2. genetic algorithm
4. Neural Networks
   1. RBF (radial basis neural net)(Broomhead and Lowe, 1988)
   2. ART (Adaptive Resonance Theory)(Carpenter and Grossberg, 1987)
      1. competitive learning
      2. online learning or incremental learning
   3. SOM(self-organizing map)(Kohonen, 1982)
   4. Cascade-Correction Net (Fahlman and Lcbiere, 1990)
   5. Elman Net (Elman, 1990)
      1. recurrent neural networks
   6. Boltzmann Machine(Actley et al, 1985)
      1. Restricted Boltzmann Machine, Contrastive Divergence Algorithm (Hinton, 2010)

Homework

1. coding: 李沐 MLP & neural nets (math and code)
   1. MLP loss vs logistic loss (形式)
2. use ChatGPT to get Restricted Boltmann Machine Derivatives (5.24)

## Chapter 6 SVM

## Chapter 7 Bayesian Classifier