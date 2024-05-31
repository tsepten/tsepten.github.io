---
layout: default
---

# Real Analysis - Riemann Integration

```
int main () {
    return 0;
}
```

Partitions of an Interval
=========================

To define the Riemann integral, we first need the concept of a partition
of an interval.

Definition
----------

A **partition** $P$ of an interval $[a, b]$ is a finite set of points
$$P = \{ x_0, x_1, x_2, \ldots, x_n \}$$ such that
$$a = x_0 < x_1 < x_2 < \cdots < x_n = b.$$

Each subinterval $[x_{i-1}, x_i]$ is called a **partition interval**.

Norm of a Partition
-------------------

The **norm** of a partition $P$, denoted by $\|P\|$, is the length of
the longest subinterval in the partition:
$$\|P\| = \max_{1 \leq i \leq n} (x_i - x_{i-1}).$$

Riemann Sums
============

Given a function $f$ defined on $[a, b]$ and a partition $P$, we can
form a Riemann sum.

Definition
----------

A **Riemann sum** of $f$ for the partition $P$ is given by
$S(P, f) = \sum_{i=1}^{n} f(t_i) (x_i - x_{i-1})$, where
$t_i \in [x_{i-1}, x_i]$ is a point chosen within each subinterval.

Riemann Integrable Functions
============================

A function $f$ is said to be Riemann integrable if the Riemann sums
converge to a single value as the norm of the partition approaches zero.

Definition
----------

A function $f$ defined on $[a, b]$ is **Riemann integrable** if for
every $\epsilon > 0$, there exists a $\delta > 0$ such that for any
partition $P$ of $[a, b]$ with $\|P\| < \delta$, and for any choice of
points $t_i \in [x_{i-1}, x_i]$,

$\left| S(P, f) - I \right| < \epsilon$, where $I$ is the value of the
integral.

Riemann Integral
----------------

The **Riemann integral** of $f$ over $[a, b]$ is denoted by
$$\int_a^b f(x) \, dx$$ and is defined as the limit of the Riemann sums:
$$\int_a^b f(x) \, dx = \lim_{\|P\| \to 0} S(P, f).$$

Properties of the Riemann Integral
==================================

Riemann integrals have several important properties, including linearity
and the ability to split the integral over adjacent intervals.

Linearity
---------

If $f$ and $g$ are Riemann integrable on $[a, b]$ and
$\alpha, \beta \in \mathbb{R}$, then
$$\int_a^b (\alpha f(x) + \beta g(x)) \, dx = \alpha \int_a^b f(x) \, dx + \beta \int_a^b g(x) \, dx.$$

Additivity
----------

If $f$ is Riemann integrable on $[a, b]$ and $[b, c]$, then
$$\int_a^c f(x) \, dx = \int_a^b f(x) \, dx + \int_b^c f(x) \, dx.$$

Comparison
----------

If $f$ and $g$ are Riemann integrable on $[a, b]$ and $f(x) \leq g(x)$
for all $x \in [a, b]$, then
$$\int_a^b f(x) \, dx \leq \int_a^b g(x) \, dx.$$
