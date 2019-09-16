# Graph Generative Networks

## Non-Learning
- Erdős, Rényi, 1960
- Barabási, Albert, 1999

## VAE:
	- T. N. Kipf and M. Welling, Variational graph auto-encoders. 2016
		- http://tkipf.github.io/graph-convolutional-networks/
		- X: N x F (features on nodes); Adj: N x N;
		- Training:
			- Encoder: a bunch of layers of non-linear(W\*Laplacian\*X), get mu and sigma;
			- Sample z from N(mu, sigma) for decoder;
			- Decoder: (Linear - ReLU) x 3;
			- Decoder output reshaped as N x N, loss with ground truth Adj-GT;
			- Additional loss of KL-Div on mu, sigma;
		- Testing: directly sampling;
		<img src="/Graph/images/gcn-vae.png" alt="drawing" width="500"/>

	- Brute-Force VAE: GraphVAE: Towards Generation of Small Graphs Using Variational Autoencoders
	- T. Ma, J. Chen, and C. Xiao, Constrained generation of semantically valid graphs via regularizing variational autoencoders. NIPS'18
	- RvNN-VAE: M Li, A Patil, K Xu, S Chaudhuri, O Khan, A Shamir, C Tu, B Chen, D Cohen-Or, H Zhang. GRAINS: Generative Recursive Autoencoders for INdoor Scenes. SIGGRAPH'19

## Autoregressive:
	- **GEG**: Y Li, O Vinyals, C Dyer, R Pascanu, P Battaglia. Learning Deep Generative Models of Graphs. ICML'18
		- (1) sample whether to add a new node of a particular type or terminate;
		- (2) we add a node of this type to the graph;
		- (3) check if any further edges are needed to connect the new node to the existing graph;
		- (4) we select a node in the graph and add an edge connecting the new node to the selected node. The algorithm goes back to step (3) and repeats until the model decides not to add another edge. 
		- Finally, the algorithm goes back to step (1) to add subsequent nodes.
	- Q Liu, M Allamanis, M Brockschmidt, and A Gaunt. Constrained Graph Variational Autoencoders for Molecule Design. NIPS'18

- **GraphRNN**: J. You, R. Ying, X. Ren, W. L. Hamilton, and J. Leskovec, GraphRNN: A deep generative model for graphs. ICML'18
	- https://github.com/snap-stanford/GraphRNN
	- Graph-level RNN;
	- Edge-level RNN; (adjacency vector)
	- Evaluation: MMD (Maximum Mean Discrepancy)

## Others
- D Johnson. Learning graphical state transitions. ICLR'17
- B. Yu, H. Yin, and Z. Zhu, Spatio-temporal graph convolutional networks: A deep learning framework for traffic forecasting. IJCAI'18
- N. De Cao and T. Kipf, Molgan: An implicit generative model for small molecular graphs. arxiv'18
- A. Bojchevski, O. Shchur, D. Zugner, and S. Gunnemann, Net-gan: Generating graphs via random walks. ICML'18