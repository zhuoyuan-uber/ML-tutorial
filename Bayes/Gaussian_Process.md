# Gaussian Process

## Good Summaries
- https://katbailey.github.io/post/gaussian-processes-for-dummies/
- http://www.gaussianprocess.org/
- https://distill.pub/2019/visual-exploration-gaussian-processes/
- Tutorials
	- MacKay, D. J. C. (1998). Introduction to Gaussian processes. In C. M. Bishop (Ed.), Neural Networks and Machine Learning, pp. 133–166. Springer. 1998
	- Williams, C. K. I. (1999). Prediction with Gaussian processes: from linear regression to linear prediction and beyond. In M. I. Jordan (Ed.), Learning in Graphical Models, pp. 599–621. MIT Press. 1999
	- MacKay, D. J. C. Information Theory, Inference and Learning Algorithms. 2003
- GP for Optimization
	- https://krasserm.github.io/2018/03/19/gaussian-processes/
	- https://zhuanlan.zhihu.com/p/86386926
	- BoTorch (Bayesian Optimzation for Pytorch): https://botorch.org/


## Textbooks 
- Kevin Murphy's textbook
	- A GP defines a **prior over functions**, which can be converted into a posterior over functions once we have seen some data. Although it might seem difficult to represent a distrubtion over a function, it turns out that we only need to be able to define a distribution over the function’s values at a finite, but arbitrary, set of points, say (x1,...,xN). 
	- A GP assumes that p(f(x1),...,f(xN)) is jointly Gaussian, with some mean μ(x) and covariance ∑(x) given by ∑ij=k(xi,xj)
	, where k is a positive definite kernel function. The key idea is that if 
	xi and xj are deemed by the kernel to be similar, then we expect the output of the function at those points to be similar, too.
	- https://github.com/probml/pmtk3
- C Rasmussen, C Williams. Gaussian Processes for Machine Learning. 2006

## PRML Bishop, Chap 6.4
- Applications:
	- kriging (Cressie, 1993)
	- ARMA (autoregressive moving average) models, Kalman filters, and radial basis function network;
- Notations: y(x) = dot(w, phi(x)), p(w) ~ N(0, alpha^(-1)I):\
	<img src="/Bayes/images/gp/gp-1.png" alt="drawing" width="400"/>
- GP for regression with noise: tn = yn + eps-n, y is noise free, t: noisy observation; marginal distribution of t:
	<img src="/Bayes/images/gp/gp-2.png" alt="drawing" width="300"/>\
	<img src="/Bayes/images/gp/gp-3.png" alt="drawing" width="400"/>
- Predict t-N+1 with x-N+1:\
	<img src="/Bayes/images/gp/gp-4.png" alt="drawing" width="250"/>\
	<img src="/Bayes/images/gp/gp-5.png" alt="drawing" width="250"/>\
	<img src="/Bayes/images/gp/gp-6.png" alt="drawing" width="450"/>
- Hyper-paramter learning: e.g., noise beta;\
	<img src="/Bayes/images/gp/gp-7.png" alt="drawing" width="400"/>
	<img src="/Bayes/images/gp/gp-8.png" alt="drawing" width="450"/>
- ARD (Automatic relevance determination):\
	<img src="/Bayes/images/gp/ard-1.png" alt="drawing" width="400"/>\
	<img src="/Bayes/images/gp/ard-2.png" alt="drawing" width="400"/>
- GP for classification:
	- Notation: logit a(x), logistic sigmoid y=simga(a):\
		<img src="/Bayes/images/gp/gp-cls-1.png" alt="drawing" width="300"/>\
		<img src="/Bayes/images/gp/gp-cls-2.png" alt="drawing" width="300"/>\
		<img src="/Bayes/images/gp/gp-cls-3.png" alt="drawing" width="300"/>\
		<img src="/Bayes/images/gp/gp-cls-4.png" alt="drawing" width="300"/>\
		<img src="/Bayes/images/gp/gp-cls-5.png" alt="drawing" width="400"/>
	- Another way: Laplacian approximation:\
		<img src="/Bayes/images/gp/gp-cls-6.png" alt="drawing" width="400"/>\
		<img src="/Bayes/images/gp/gp-cls-7.png" alt="drawing" width="400"/>\
		<img src="/Bayes/images/gp/gp-cls-8.png" alt="drawing" width="400"/>
- Connection with NN: for a broad class of prior distributions over w, the distribution of functions generated by a neural network will tend to a Gaussian process in the limit M approaches infitnity;
	- Neal, R. M. Bayesian Learning for Neural Networks. Springer. Lecture Notes in Statistics 118. 1996

## Theory
- D R. Burt, C E. Rasmussen, M van der Wilk. Rates of Convergence for Sparse Variational Gaussian Process Regression. ICML'19 best paper
	- Reduce O(NM^2+M^3) to  and O(NM+M^2)

## Deep GP
- Neil D Lawrence and Andrew J Moore. Hierarchical gaussian process latent variable models. ICML'07
- Andreas Damianou and Neil Lawrence. Deep gaussian processes. AISTATS'13
- David Duvenaud, Oren Rippel, Ryan Adams, and Zoubin Ghahramani. Avoiding pathologies in very deep networks. AISTATS'14
- Thang Bui, Daniel Herna ́ndez-Lobato, Jose Hernandez-Lobato, Yingzhen Li, and Richard Turner. Deep gaussian processes for regression using approximate expectation propagation. ICML'16

## Connection with Neural Network
- Radford M. Neal. Priors for infinite networks. 1994
	- Single hidden layer
- Radford M. Neal. Bayesian Learning for Neural Networks. 1994
- Christopher KI Williams. Computing with infinite networks. NIPS'97
- Jaehoon Lee, Yasaman Bahri, Roman Novak, Samuel S. Schoenholz, Jeffrey Pennington, Jascha Sohl-Dickstein. Deep Neural Networks as Gaussian Processes. ICLR'18
	- Exact equivalence between infinitely wide deep networks and GPs
	- Focus on exact Bayesian inference for regression tasks
	- https://github.com/brain-research/nngp

## Unclassified
- Orthogonally Decoupled Variational Gaussian Processes. NIPS'18
- Infinite-Horizon Gaussian Processes. NIPS'18
- Learning Gaussian Processes by Minimizing PAC-Bayesian Generalization Bounds. NIPS'18

## NIPS'19
- Haibin YU, Yizhou Chen, Bryan Kian Hsiang Low, Patrick Jaillet, Zhongxiang Dai. Implicit Posterior Variational Inference for Deep Gaussian Processes
- Rui Li. Multivariate Sparse Coding of Nonstationary Covariances with Gaussian Processes
- Siqi Liu, Milos Hauskrecht. Nonparametric Regressive Point Processes Based on Conditional Gaussian Processes
- Ian Char, Youngseog Chung, Willie Neiswanger, Kirthevasan Kandasamy, Oak Nelson, Mark Boyer, Egemen Kolemen, Jeff Schneider. Offline Contextual Bayesian Optimization
- Creighton Heaukulani, Mark van der Wilk. Scalable Bayesian dynamic covariance modeling with variational Wishart and inverse Wishart processes
- Yusuke Tanaka, Toshiyuki Tanaka, Tomoharu Iwata, Takeshi Kurashima, Maya Okawa, Yasunori Akagi, Hiroyuki Toda. Spatially Aggregated Gaussian Processes with Multivariate Areal Outputs
- Armin Lederer, Jonas Umlauft, Sandra Hirche. Uniform Error Bounds for Gaussian Process Regression with Application to Safe Control
