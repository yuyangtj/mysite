---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Multivariate Gaussian Distribution"
subtitle: ""
summary: ""
authors: []
tags: [numpy, statitics]
categories: []
date: 2019-06-29T08:30:11+02:00
lastmod: 2019-06-29T08:30:11+02:00
featured: false
draft: false

# ```python
# #plot Multivariate gaussian 
# #using tensor contraction (mnn)(mm)(mnn)->nn, which gives 'i...,ii,i...'
# #n is the # of variates, and m is the # of observations

# import numpy as np
# import matplotlib.pyplot as plt
# x = np.linspace(-1000,1000,300)
# x1, x2 = np.meshgrid(x, x)
# covariance_matrix = np.identity(2)
# mu = np.array([-400,300])
# density_matrix=np.einsum('i...,ii,i...', np.array([x1-mu[0],x2-mu[1]]), covariance_matrix, np.array([x1-mu[0],x2-mu[1]]))
# plt.contourf(x1, x2, density_matrix)
# plt.show()
# ```

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
projects: []



---

Multivariate gaussian model

$$f_\boldsymbol{x}(x_1, x_2,..., x_n) \propto \mathrm{exp}(-\frac{1}{2}(\boldsymbol{x}-\boldsymbol{\mu})^\mathrm{T}\boldsymbol{\Sigma}^{-1}(\boldsymbol{x}-\boldsymbol{\mu})),$$

and the normalization factor is given by $$\frac{1}{\sqrt{(2 \pi)^k} \mathrm{det}(\boldsymbol{\Sigma})}.$$


```python
#plot Multivariate gaussian 
#using tensor contraction (imn)(ij)(jmn)->mn, which gives 'i...,ij,j...'
#i (= j) is the # of variates, (m,n) is the # of grid points, 
#where the probability density function is calculated

import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-4,4,200)
x1, x2 = np.meshgrid(x, x)
covar = np.array([[[1,0], [0, 1]],[[0.2,0], [0, 1]],[[0.2,-0.4], [-0.4, 1]],[[0.2,.4], [.4, 1]]])
mu_vec = np.array([1,1])
shifted_mu_vec = np.array([x1-mu_vec[0],x2-mu_vec[1]])
for i in range(4):
    tensor_contraction=np.einsum('i...,ij,j...', shifted_mu_vec, np.linalg.inv(covar[i]), shifted_mu_vec)
    density_matrix = np.exp(-0.5*tensor_contraction)
    plt.subplot(2,2, i+1)
    plt.contourf(x1, x2, density_matrix, cmap = 'jet')   
    plt.title('covariance_matrix=%s' % covar[i].tolist())
plt.show()


```
![](mvn.png)