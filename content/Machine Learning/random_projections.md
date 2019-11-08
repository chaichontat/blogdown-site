---
title: "Random Projection"
section: "Machine Learning"
author: "Chaichontat Sriworarat"
date: 2019-11-07
tags: ["math", "ml"]
---

$$
% Containers
\newcommand{\pp}[1]{\left(#1\right)}
\newcommand{\bk}[1]{\left[#1\right]}
\newcommand{\b}[1]{\mathbf{#1}}
\newcommand{\bs}[1]{\boldsymbol{#1}}
\newcommand{\on}[1]{\opertorname{#1}}
\newcommand{\expb}[1]{\, \exp\left\{#1\right\}}

% Abbreviations
\newcommand{\summ}{\sum_{i=1}^n}
\newcommand{\prodd}{\prod_{i=1}^n}
\newcommand{\xdots}{x_1, \dots, x_n}
\newcommand{\T}{\mathsf{T}}
\newcommand{\normal}[1]{\mathcal{N}\left(#1\right)}
\newcommand{\real}{\mathbb{R}}
\newcommand{\Pr}[1]{\mathrm{Pr} \left(#1\right)}
\newcommand{\abs}[1]{\left|#1\right|}
\newcommand{\norm}[1]{\left\|#1\right\|}

% Functionals
\newcommand{\E}[1]{\mathbb{E}\left[#1\right]}
\newcommand{\Var}[1]{\operatorname{Var}\left[#1\right]}
$$

### Near-orthogonality
There could be at most $D$ orthogonal vectors in $\real^{D}$. However, if we relax this constrain to allow vectors that are  $ϵ$-orthogonal, there are exponential of them.

### Random Vector
Let $\b{v}$ be a random vector of length $n$ with each component being $v_i \sim \normal{0, 1}$. The normal distribution has many useful properties, one of the most important being closure under scalar multiplication and addition.

Define another random variable
$$
\begin{align}
  Y &= X_1 + X_2 + \dots + X_n \\
  &\sim \chi^2_n
\end{align}
$$
The expectation of $Y$ is
$$
\begin{align}
  \E{Y} &= \summ \E{X_i^2} \\
  &= \summ \Var{X_i}+\E{X_i}^2 &\text{Property of variance} \\
  &= n
\end{align}
$$
The concentration inequality is
$$
\begin{align}
  P(|Y-k| \geq \epsilon) \leq 2 e^{-k\epsilon^2/8}
\end{align}
$$

Knowing that
$$
\begin{align}
  \frac{\norm{A\b{x}}^2}{\norm{\b{x}}} &\sim \chi^2_k
\end{align}
$$
leads to
$$
\begin{align}
  \Pr{\abs{1-\frac{\norm{F_A(\b{x})}^2}{\norm{x}^2}}\geq\delta} \leq 2 \expb{-\frac{kδ^2}{8}}
\end{align}
$$


### Johnson-Lindenstrauss Lemma
Fix $k \in \real^+$
$$
\begin{align}
  k > \frac{16}{\delta^2} \, \log\pp{\frac{n}{\sqrt{\epsilon}}}
\end{align}
$$
Define $\b{A}$ as a $k \times D$ random matrix.
$$
\begin{align}
  A_{i,j} &\sim \normal{0,1} \\
  F_A(\b{z}) &= \frac{\b{A}}{\sqrt{k}}\b{z}
\end{align}
$$
Then for each pair $i, j: i≠j$
$$
\begin{align}
  \Pr{\abs{1-\frac{\norm{F_A(\b{z}_i)-F_A(\b{z}_j)}}{\norm{\b{z}_i-\b{z}_j}}}\geq\delta} \leq \frac{2\epsilon}{n^2}
\end{align}
$$

To calculate the probability that _any_ pairs will violate the probability, we use the union bound,
$$
\begin{align}
  \Pr{\bigcup_{i≠j} \, x_{ij}} &≤ \sum_{i≠j} \Pr{x_{ij}} \\
  &= \frac{n(n-1)}{2}\ \frac{2\epsilon}{n^2} \\
  &< \epsilon
\end{align}
$$