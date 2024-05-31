---
layout: default
title: "Real Analysis"
permanlinks: /notes/real-analysis/
---

# Real Analysis

## Lecture 1

### Topic 1: Introduction to Real Analysis

Content for topic 1...

### Topic 2: Sequences and Limits

Consider the sequence \(a_n\) defined by \(a_n = \frac{1}{n}\). We want to show that \(a_n\) converges to 0 as \(n\) approaches infinity.

#### Definition

A sequence \( \{a_n\} \) converges to a limit \( L \) if for every \( \epsilon > 0 \), there exists an \( N \in \mathbb{N} \) such that for all \( n \geq N \), \( |a_n - L| < \epsilon \).

## Lecture 2

### Topic 1: Continuity

A function \( f \) is continuous at a point \( x = a \) if the limit of \( f(x) \) as \( x \) approaches \( a \) is equal to \( f(a) \). Mathematically,

\[
\lim_{{x \to a}} f(x) = f(a)
\]

### Topic 2: Differentiability

A function \( f \) is differentiable at a point \( x = a \) if the derivative \( f'(a) \) exists. The derivative is defined as

\[
f'(a) = \lim_{{h \to 0}} \frac{f(a + h) - f(a)}{h}
\]


# Math of Data Science Test

**Homework 3**

1.  Download the dataset `genomedata.mat` from Canvas; it contains
    Single Nucleid Polymorphism data from the Human Genome Diversity
    Project. The data consists of an array with 5000 rows, where each
    row has 1043 different strings. The 5000 rows are Single Nucleid
    Polymorphisms, and the columns correspond to 1043 different
    individuals. The entries are not numerical values (quite
    annoyingly), but contain the characters
    'AA','CC','GG','TT','AG','AC','TC','TG', and (even more annoyingly)
    also '`–`', which represents missing measurements. Your goal is to
    cluster the data into a small number of clusters. Before trying to
    cluster the data, you need to convert the characters into numerical
    values. It is up to you which conversion you use. The so-called
    "one-hot" encoding method is one choice, but maybe there are better
    ones for this case? (I do not know, but it is worth considering.)

    Since the data are high-dimensional you first need to reduce the
    dimension before clustering. You should attempt the dimension
    reduction via PCA as well as via diffusion maps. In both cases you
    need to decide how many dimensions you want to use. (Results may
    vary depending on your choice of conversion rule. However, you
    likely will not get a meaningful clustering via PCA, but hopefully
    will get something reasonable with diffusion maps.)

    **Solution:**

    We download the dataset, import it, and then convert it into
    suitable format for analysis by converting our labels such as AA,
    CC, etc. into a numerical format using one-hot-encoding. Prior to
    clustering, we attempt dimnsion reduction via PCA and via a
    diffusion map. For PCA, we decide to reduce down into 50 components
    in order to capture a decent amount of variance. For our diffusion
    map, we use only 10 components sincewe assume this is enough to
    capture the non-linear structure of the data. These parameters can
    be experimented with using methods like the Elbow method.
    Afterwards, we run K-means of 5 clusters on both. Lastly, we
    visualize our clusters and utilize some popular evaluation metrics
    such as silhoutte and Davies bouldin score. Our PCA returns a
    Silhoutte score of **0.358** and a Davies-Bouldin index of
    **1.114**. Our diffusion map returns a Silhoutte score of **0.544**
    and a Davies-Bouldin index of **0.645**. A higher Silhoutte score
    closer to 1 indicates better clustering, and a lower Davies-Bouldin
    score indicates better clustering. In both scores, our diffusion map
    does better by a decent margin.

    ![image](fig1.png){width="1\\columnwidth"}

    The visualization indicates that our diffusion map does indeed seem
    to work better. For our PCA clusters (left plot), the x-axis
    represents the first principal component, and the y-axis the second
    principal component. The plot shows distinct clusters however there
    seeems to be some overlap between them. Our diffusion map clustere
    has x-axis representing the first diffusion map component, and the
    y-axis representing the seceond diffusion map component. This plot
    shows more distinct and properely separated clusteers indicating
    that our diffusion map is more effective than using PCA.

    The code is attached
    [here](https://drive.google.com/file/d/1frnIutH3QZUwDUPr4435SGmqKduzmeQH/view?usp=sharing).

2.  Recall that the Johnson--Lindenstrauss lemma states that the
    geometry of the data is well preserved when we project onto a random
    subspace of dimension $m \asymp \log n$. In this problem, we will
    show that this dependency is optimal.

    Consider the set $\chi=\{0,e_1,\ldots,e_{n-1}\}$ of $n$ points in
    $\mathbb{R}^n$, where $e_i$ is the $i$-th standard basis vector.
    Show that no linear map $\mathbb{R}^n \to \mathbb{R}^m$ can be an
    $\varepsilon$-isometry for $\varepsilon = 1/10$ if
    $m/\log n \rightarrow 0$ as $n \to \infty$.

    *Hint: Use a volume argument to limit the number of points inside an
    $m$-dimensional ball such that each pair is "far" apart.*

    **Solution:** Define set $\chi = \{0, e_1, \ldots, e_{n-1}\}$ of $n$
    points in $\mathbb{R}^n$, where $e_i$ is the $i$-th standard basis
    vector. We need to show that no linear map
    $\mathbb{R}^n \to \mathbb{R}^m$ can be an $\varepsilon$-isometry for
    $\varepsilon = 1/10$ if $m/\log n \rightarrow 0$ as $n \to \infty$.

    A map $f: \mathbb{R}^n \to \mathbb{R}^m$ is an
    $\varepsilon$-isometry if for all $x, y \in \mathbb{R}^n$,
    $$(1 - \varepsilon) \|x - y\| \leq \|f(x) - f(y)\| \leq (1 + \varepsilon) \|x - y\|.$$
    For $\varepsilon = 1/10$, this means the distances are preserved by
    factor $1 \pm 0.1$.

    So in the set $\chi = \{0, e_1, \ldots, e_{n-1}\}$, we have that
    $$\|0 - e_i\| = 1 \quad \text{for all } i, \text{ and } \|e_i - e_j\| = \sqrt{2} \quad \text{for all } i \neq j.$$

    Now we consider the image of $\chi$ under a linear map
    $f: \mathbb{R}^n \to \mathbb{R}^m$. Each point $f(e_i)$ should lie
    on the surface of an $m$-dimensional sphere of radius
    $(1 \pm \varepsilon)$ centered at $f(0)$. Since $f$ is linear,
    $f(0) = 0$ and $\|f(e_i)\| \approx 1$.

    The volume of an $m$-dimensional ball of radius $1 + \varepsilon$ is
    proportional to $(1 + \varepsilon)^m$. To have $n$ points with the
    distances between each preserved (isometry), the number of points
    essentially should not exceed the packing or covering number (the
    maximum number of disjoint balls of a certain radius that can fit
    inside a larger ball).

    For points to be $\varepsilon$-isometric, the distance
    $\|f(e_i) - f(e_j)\|$ should be around $\sqrt{2}$. Consider the
    volume of a small ball of radius $\sqrt{2}(1 - \varepsilon)$ which
    scales as
    $(\sqrt{2}(1 - \varepsilon))^m = 2^{m/2}(1 - \varepsilon)^m$.
    Therefore the number of such small balls that fit into a ball of
    radius $(1 + \varepsilon)$ is roughly:
    $$\frac{(1 + \varepsilon)^m}{2^{m/2}(1 - \varepsilon)^m} = \left( \frac{1 + \varepsilon}{\sqrt{2}(1 - \varepsilon)} \right)^m.$$
    For small $\varepsilon$, this ratio is approximately
    $(1 + \varepsilon/\sqrt{2})^m$.

    To fit $n$ points, the number of such disjoint small balls must be
    at least $n$:
    $$n \leq \left( \frac{1 + \varepsilon}{\sqrt{2}(1 - \varepsilon)} \right)^m.$$
    Take log,
    $$\log n \leq m \log \left( \frac{1 + \varepsilon}{\sqrt{2}(1 - \varepsilon)} \right).$$
    For $\varepsilon = 1/10$,
    $\log \left( \frac{1 + \varepsilon}{\sqrt{2}(1 - \varepsilon)} \right) \approx \log \left( \frac{1.1}{0.9\sqrt{2}} \right)$.
    If $m / \log n \to 0$, then $n$ grows faster than $m$, which
    contradicts the inequality above.

    Therefore, no linear map $\mathbb{R}^n \to \mathbb{R}^m$ can be an
    $\varepsilon$-isometry for $\varepsilon = 1/10$ if $m/\log n \to 0$
    as $n \to \infty$. This shows that the dependency $m \asymp \log n$
    is optimal for preserving the geometry of the data.

3.  Suppose I want to carry out a dimension reduction
    $\mathbb{R}^p \to \mathbb{R}^d$ via the map $\frac{1}{a_d}G$ from
    Gordon's theorem. If I want to use Gordon's theorem to ensure that I
    preserve the norm of every vector in the hypercube
    $\{\pm 1/\sqrt{p}\}^p$ up to a factor $1 \pm 1/100$, how large
    should $d$ be? You may give an approximate asymptotic answer for
    large $p$, such as $\Theta(\log p)$ or $\Theta(\sqrt{p})$. Does this
    allow a significant reduction in dimension?

    **Solution:** Recall that Gordon's theorem gives bounds on the
    singular values of Gaussian random matrices. So if $G$ is a
    $d \times p$ matrix with entries being independent standard normal
    random variables, then the map $\frac{1}{a_d} G$, where
    $a_d = \sqrt{d}$, we can use for dimension reduction from
    $\mathbb{R}^p$ to $\mathbb{R}^d$.

    We want to ensure that for every vector $x$ in the hypercube
    $\{\pm 1/\sqrt{p}\}^p$,
    $$(1 - \frac{1}{100}) \|x\| \leq \left\| \frac{1}{\sqrt{d}} G x \right\| \leq (1 + \frac{1}{100}) \|x\|.$$

    First, consider the norm of vectors in the hypercube
    $\{\pm 1/\sqrt{p}\}^p$:
    $$\|x\|^2 = \sum_{i=1}^p \left( \pm \frac{1}{\sqrt{p}} \right)^2 = \sum_{i=1}^p \frac{1}{p} = 1.$$
    Thus, each vector in the hypercube has a norm of 1.

    When we apply the map $\frac{1}{\sqrt{d}} G$, the resulting norm is
    determined by the properties of the Gaussian random matrix $G$. So
    we need to consider the concentration of measure and the
    Johnson-Lindenstrauss lemma, which helps us understand the required
    dimension $d$ for preserving norms.

    Again recall that the Johnson-Lindenstrauss lemma states that for
    any $0 < \epsilon < 1$, and for any set of $n$ points in
    $\mathbb{R}^p$, there exists a linear map
    $f : \mathbb{R}^p \to \mathbb{R}^d$ such that:
    $$(1 - \epsilon) \|x - y\| \leq \|f(x) - f(y)\| \leq (1 + \epsilon) \|x - y\|$$
    for all pairs of points $x$ and $y$. The required dimension $d$ is
    given by:
    $$d \geq \frac{4 \log n}{\epsilon^2 / 2 - \epsilon^3 / 3}.$$

    In our case, $\epsilon = \frac{1}{100}$, and we need to find the
    dimension $d$ such that the norms of all vectors in the hypercube
    $\{\pm 1/\sqrt{p}\}^p$ are preserved within a factor of
    $1 \pm \frac{1}{100}$. Given the hypercube has $2^p$ vertices,
    $n = 2^p$. Thus, plugging in the values, we have:
    $$\epsilon = \frac{1}{100}, \quad n = 2^p.$$

    Now using the Johnson-Lindenstrauss bound
    $$d \geq \frac{4 \log (2^p)}{\left( \frac{1}{100} \right)^2 / 2 - \left( \frac{1}{100} \right)^3 / 3}.$$
    Simplifying\...
    $$d \geq \frac{4 p \log 2}{\frac{1}{20000} - \frac{1}{3000000}}.$$
    Approximating:
    $$\frac{1}{20000} - \frac{1}{3000000} \approx \frac{1}{20000},$$ so:
    $$d \geq \frac{4 p \log 2 \cdot 20000}{1} \approx 80000 p \log 2.$$

    Thus we have that: $$d = \Theta(p).$$

    To ensure the preservation of the norm of every vector in the
    hypercube $\{\pm 1/\sqrt{p}\}^p$ up to a factor of
    $1 \pm \frac{1}{100}$, the required dimension $d$ should be
    approximately $\Theta(p)$. This means that though there exists some
    reduction in dimension from $p$ to $d$, it is not significant
    compared to the initial dimnsion $p$ since it scales linearly with
    $p$.
