---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Expectation Minimization"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2019-08-18T21:05:29+02:00
lastmod: 2019-08-18T21:05:29+02:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.

#$$p(j{\mid}i) = \frac{p_jN(x^(i){\mid}u_j,\sigma_{j}I^2)}{\sum_j{p_j N(x^(i){\mid}u_j,\sigma_{j}I^2)}}$$
projects: []
---
Visualization of EM (Expectation-Minimization) algorithm.

![](giphy.gif)

naive version
E-step:

get the conditional probability 

$$ \frac{p_{j}\mathcal{N}(x^{(i)}{\mid}\mu_j,\sigma_jI^2)}{\sum_jp_j\mathcal{N}(x^{(i)}{\mid}\mu_j,\sigma_jI^2)} $$

assign the class, and $\delta(j{\mid}i)=1$ indicate the test point $x^{(i)}$ was assigned to the class $j$.

calculate the log-likelihood

$$\sum_j\sum_i\delta(j{\mid}i)*\mathrm{log}(p_j\mathcal{N}(x^{(i)}{\mid}\mu_j,\sigma_jI^2))$$

update $p_j$, $\mu_j$, and $\sigma_j$

$$\hat{n}_j = \sum_i\delta(j{\mid}i)$$ 
$$\hat{p}_j = \frac{\hat{n}_j}{n}$$ 
$$\hat{\mu}_j = \frac{1}{\hat{n}_j}\sum_i\delta(j{\mid}i)x^{(i)}$$ 
$$\hat{\sigma}^2_j = \frac{1}{\hat{n}_jd}\sum_i\delta(j{\mid}i){\Vert}x^{(i)}-\mu_j{\Vert}^2$$

Each symbol represents the conditional probabilities $$p(y=k{\mid}x; \theta)$$
and $$\sum_{k\in(R, B, G)}{p(y=k{\mid}x; \theta)}=1$$

Ellipses represent the 2D Gaussian contour, which captures >99.7% probabilities of the associated Gaussian distribution.