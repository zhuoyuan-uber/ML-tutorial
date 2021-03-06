# Information Theory in Machine Learning

## Books
- David JC MacKay. Information theory, inference and learning algorithms. Cambridge university press, 2003.

## Basics
- Markov Chain
- Kullback–Leibler (KL) Divergence;
- F-divergence: more general:\
	<img src="/DL/images/info-theory/f-div1.png" alt="drawing" width="400"/>\
	<img src="/DL/images/info-theory/f-div2.png" alt="drawing" width="350"/>
- Mutual Information: I(X; Y)
	- I(X;Z) = H(X) - H(X|Z);
	- Connection with KL:\
		<img src="/DL/images/info-theory/mi.png" alt="drawing" width="350"/>
	- DV or Donsker-Varadhan representation: dual form;\
		<img src="/DL/images/info-theory/dv.png" alt="drawing" width="350"/>
	- Proof by construction: when G=P, gap is zero;\
		<img src="/DL/images/info-theory/dv-dual.png" alt="drawing" width="450"/>
	- Data Processing Inequality (DPI): X->Y->Z, then I(X;Y)>=I(X;Z)
	- Reparametrization invariance: Two invertible functions f1, f2, then I(X;Y)=I(f1(X);f2(Y))
- Information Plane Theorem:
	- X-axis: The sample complexity of Ti is determined by the encoder mutual information I(X;Ti). Sample complexity refers to how many samples you need to achieve certain accuracy and generalization.
	- Y-axis: The accuracy (generalization error) is determined by the decoder mutual information I(Ti;Y).\
		<img src="/DL/images/info-theory/info-plane.png" alt="drawing" width="450"/>

## Classical
- **IB**: N. Tishby, F.C. Pereira, and W. Biale. The information bottleneck method. Allerton'99
- William Bialek, Ilya Nemenman, and Naftali Tishby. Predictability, complexity, and learning. Neural computation'01
- Susanne Still and William Bialek. How many clusters? an information-theoretic perspective. Neural computation'04
- David Barber Felix Agakov. The IM algorithm: a variational approach to information maximization. NIPS'04
- Noam Slonim, Gurinder Singh Atwal, Gasˇper Tkacˇik, and William Bialek. Information-based clustering. PNAS'05
- Ohad Shamir, Sivan Sabato, and Naftali Tishby. Learning and generalization with the information bottleneck. Theoretical Computer Science'10
- Stephanie E Palmer, Olivier Marre, Michael J Berry, and William Bialek. Predictive information in a sensory population. PNAS'15

## Deep Learning
- N. Tishby and N. Zaslavsky. Deep learning and the information bottleneck principle. In IEEE Information Theory Workshop, 2015
- Alessandro Achille and Stefano Soatto. Information dropout: Learning optimal representations through noisy computation. 2016.
- **DVIB**: A Alemi, I. Fischer, J V. Dillon, K Murphy. Deep Variational Information Bottleneck. ICLR'17
	- Formulation:\
		<img src="/Basic-ML/images/info-theory/dvib-1.png" alt="drawing" width="450"/>
	- The first term in RIB encourages Z to be predictive of Y;
	- The second term encourages Z to "forget" X;
	- Essentially it forces Z to act like a minimal sufficient statistic of X for predicting Y;
	- Formulation: we assume p(Z|X,Y) = p(Z|X), corresponding to the Markov chain Y ↔ X ↔ Z. This restriction means that our representation Z cannot depend directly on the labels Y. This opens the door to **unsupervised representation learning**;
	- I(z;y) lower-bound:\
		<img src="/Basic-ML/images/info-theory/dvib-2.png" alt="drawing" width="450"/>
	- I(z;x) upper-bound:\
		<img src="/Basic-ML/images/info-theory/dvib-3.png" alt="drawing" width="450"/>
	- Put together:\
		<img src="/Basic-ML/images/info-theory/dvib-4.png" alt="drawing" width="450"/>
	- Results on mnist: different classes;\
		<img src="/Basic-ML/images/info-theory/dvib-5.png" alt="drawing" width="450"/>
	- Connection with VAE: no Y, just index i=1/N, each item a class, then:\
		<img src="/Basic-ML/images/info-theory/dvib-6.png" alt="drawing" width="450"/>
- Gabriel Pereyra, George Tuckery, Jan Chorowski, and Lukasz Kaiser. Regularizing neural networks by penalizing confident output predictions. ICLRW'17
- Theory on DL:
	- R. Shwartz-Ziv and N. Tishby. Opening the black box of deep neural networks via information. arXiv preprint arXiv:1703.00810, 2017
		- Deep networks undergo two distinct phases consisting of an initial fitting phase and a subsequent compression phase;
		- the compression phase is causally related to the excellent generalization performance of deep networks; 
		- the compression phase occurs due to the diffusion-like behavior of stochastic gradient descen
	- Andrew Michael Saxe, Yamini Bansal, Joel Dapello, Madhu Advani, Artemy Kolchinsky, Brendan Daniel Tracey, David Daniel Cox. On the Information Bottleneck Theory of Deep Learning. ICLR'18
- IM Estimation:
	- Nowozin, S., Cseke, B., and Tomioka, R. f-gan: Training generative neural samplers using variational divergence minimization. NIPS'16
	- **MINE**: Ishmael Belghazi, Aristide Baratin, Sai Rajeswar, Sherjil Ozair, Yoshua Bengio, Aaron Courville, and R Devon Hjelm. Mine: mutual information neural estimation. ICML'18
		- Problem setup: estimate MI;
		- Key insight: use the upper bound by **dual representations of the KL-divergence**, a neural discriminator d(x;z);
		- Upper bound with neural approximation:\
			<img src="/Basic-ML/images/info-theory/mine-1.png" alt="drawing" width="450"/>
		- Algorithm:\
			<img src="/Basic-ML/images/info-theory/mine-2.png" alt="drawing" width="350"/>
		- Application: maximize MI to improve GAN on mode-collapse;
			<img src="/Basic-ML/images/info-theory/mine-3.png" alt="drawing" width="350"/>
- SSL:
	- **DIM**: R Devon Hjelm, Alex Fedorov, Samuel Lavoie-Marchildon, Karan Grewal, Phil Bachman, Adam Trischler, Yoshua Bengio. Learning deep representations by mutual information estimation and maximization. ICLR'19
		- https://github.com/rdevon/DIM
		- Problem setup: unsupervised learning;
		- Model:\
			<img src="/Basic-ML/images/info-theory/dim-1.png" alt="drawing" width="450"/>
		- Formulation:
			- **Mutual information maximization**: Find the set of parameters, phi, such that the mutual information, I(X;E(phi(X))), is maximized. Depending on the end-goal, this maximization can be done over the complete input, X, or some structured or "local" subset;
			- **Statistical constraints**: Depending on the end-goal for the representation, the marginal U(phi,P) should match a prior distribution, V. Roughly speaking, this can be used to encourage the output of the encoder to have desired characteristics (e.g., independence).
			- Put together: 1st/2nd terms for global/local MI with neural classifier parametrized by w1, w2; 3rd term discriminator with phi for statistical matching with prior;\
				<img src="/Basic-ML/images/info-theory/dim-5.png" alt="drawing" width="400"/>
		- Different ways to estimate MI:
			- MINE: based on DV (Donsker-Varadhan representation)\
				<img src="/Basic-ML/images/info-theory/dim-2.png" alt="drawing" width="400"/>
			- JS-MI:\
				<img src="/Basic-ML/images/info-theory/dim-3.png" alt="drawing" width="400"/>
			- InfoNCE:\
				<img src="/Basic-ML/images/info-theory/dim-4.png" alt="drawing" width="400"/>
	- **AMDIM**: Philip Bachman, R Devon Hjelm, William Buchwalter. Learning Representations by Maximizing Mutual Information Across Views. NIPS'19
		- https://github.com/Philip-Bachman/amdim-public
		- Problem setup: unsupervised learning;
		- Insight: maximizing mutual information between features extracted from multiple views of a shared context;

## NIPS'19
- Aditya Gangrade, Praveen Venkatesh, Bobak Nazer, Venkatesh Saligrama. Efficient Near-Optimal Testing of Community Changes in Balanced Stochastic Block Models
- Jayadev Acharya, Sourbh Bhadane, Piotr Indyk, Ziteng Sun. Estimating Entropy of Distributions in Constant Space
- Jie Ding, Robert Calderbank, Vahid Tarokh. Gradient Information for Representation and Modeling
- Dong Liu, Haochen Zhang, Zhiwei Xiong. On The Classification-Distortion-Perception Tradeoff
- Lingxiao Wang, Zhuoran Yang, Zhaoran Wang. Statistical-Computational Tradeoff in Single Index Models
- Saurabh Sihag, Ali Tajer. Structure Learning with Side Information: Sample Complexity
- Benjamin Aubin, Bruno Loureiro, Antoine Maillard, Florent Krzakala, Lenka Zdeborová. The spiked matrix model with generative priors
- Yihan Jiang, Hyeji Kim, Himanshu Asnani, Sreeram Kannan, Sewoong Oh, Pramod Viswanath. Turbo Autoencoder: Deep learning based channel codes for point-to-point communication channels

## Information Theory in DL
- Resources:
	- https://lilianweng.github.io/lil-log/2017/09/28/anatomize-deep-learning-with-information-theory.html
	- Information Theory in Deep Learning (Youtube): https://www.youtube.com/watch?v=bLqJHjXihK8&feature=youtu.be
- Two Optimization Phases:
	- Among early epochs, the mean values are three magnitudes larger than the standard deviations. After a sufficient number of epochs, the error saturates and the standard deviations become much noisier afterward. The further a layer is away from the output, the noisier it gets, because the noises can get amplified and accumulated through the back-prop process (not due to the width of the layer).
		<img src="/DL/images/info-theory/two-opt-phase.png" alt="drawing" width="450"/>
- Learning Theory:
	- Old Generalization Bounds:
		- Read https://mostafa-samir.github.io/ml-theory-pt1/ and https://mostafa-samir.github.io/ml-theory-pt2/ for ML theory;
			<img src="/DL/images/info-theory/old-bound.png" alt="drawing" width="450"/>
	- New Input compression bound:\
			<img src="/DL/images/info-theory/new-bound.png" alt="drawing" width="450"/>
- Alemi, A. A., Poole, B., Fischer, I., Dillon, J. V., Saurous, R. A., and Murphy, K. An information-theoretic analysis of deep latent-variable models. 2017
- Marylou Gabrié, Andre Manoel, Clément Luneau, Jean Barbier, Nicolas Macris, Florent Krzakala, Lenka Zdeborová. Entropy and mutual information in models of deep neural networks. NIPS'18
