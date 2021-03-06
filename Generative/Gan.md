# General Adversarial Net

## Unclassified
- NIPS'19 oral:
	- Multi-marginal Wasserstein GAN. NIPS'19
- **Causal InfoGAN**: Thanard Kurutach, Aviv Tamar, Ge Yang, Stuart Russell, Pieter Abbeel. Learning Plannable Representations with Causal InfoGAN. NIPS'18
- Michael Arbel, Dougal J. Sutherland, Mikolaj Binkowski, Arthur Gretton. On gradient regularizers for MMD GANs. NIPS'18
- Haoye Dong, Xiaodan Liang, Ke Gong, Hanjiang Lai1, Jia Zhu, Jian Yin. Soft-Gated Warping-GAN for Pose-Guided Person Image Synthesis. NIPS'18
- Chenshen Wu, Luis Herranz, Xialei Liu, Yaxing Wang, Joost van de Weijer, Bogdan Raducanu. Memory Replay GANs: Learning to Generate New Categories without Forgetting. NIPS'18
- Chang Xiao, Peilin Zhong, Changxi Zheng. BourGAN: Generative Networks with Metric Embeddings. NIPS'18
- Xiaojie Wang, Rui Zhang, Yu Sun, Jianzhong Qi. KDGAN: Knowledge Distillation with Generative Adversarial Networks. NIPS'18
- Xinyu Gong, Shiyu Chang, Yifan Jiang, Zhangyang Wang. AutoGAN: Neural Architecture Search for Generative Adversarial Networks. ICCV 2019
	- https://github.com/TAMU-VITA/AutoGAN
- Dong Wook Shu, Sung Woo Park, and Junseok Kwon. 3D Point Cloud Generative Adversarial Network Based on Tree Structured Graph Convolutions. ICCV'19
	- https://github.com/seowok/TreeGAN
- Specifying Object Attributes and Relations in Interactive Scene Generation. ICCV'19
- Counterfactual Critic Multi-Agent Training for Scene Graph Generation. ICCV'19
- 3D:
	- Neural 3D Morphable Models: Spiral Convolutional Networks for 3D Shape Representation Learning and Generation. ICCV'19
- CompoNet: Learning to Generate the Unseen by Part Synthesis and Composition. ICCV'19
- ClothFlow: A Flow-Based Model for Clothed Person Generation. ICCV'19
- Boundless: Generative Adversarial Networks for Image Extension. ICCV'19
- DUAL-GLOW: Conditional Flow-Based Generative Model for Modality Transfer. ICCV'19

## GAN of different Forms
*Name* | *Paper Link* | *Value Function*
:---: | :---: | :--- |
**GAN** | [Arxiv](https://arxiv.org/abs/1406.2661) | <img src = '/Generative/images/equations/GAN.png' height = '70px'>
**LSGAN**| [Arxiv](https://arxiv.org/abs/1611.04076) | <img src = '/Generative/images/equations/LSGAN.png' height = '70px'>
**WGAN**| [Arxiv](https://arxiv.org/abs/1701.07875) | <img src = '/Generative/images/equations/WGAN.png' height = '105px'>
**WGAN_GP**| [Arxiv](https://arxiv.org/abs/1704.00028) | <img src = '/Generative/images/equations/WGAN_GP.png' height = '70px'>
**DRAGAN**| [Arxiv](https://arxiv.org/abs/1705.07215) | <img src = '/Generative/images/equations/DRAGAN.png' height = '70px'>
**CGAN**| [Arxiv](https://arxiv.org/abs/1411.1784) | <img src = '/Generative/images/equations/CGAN.png' height = '70px'>
**infoGAN**| [Arxiv](https://arxiv.org/abs/1606.03657) | <img src = '/Generative/images/equations/infoGAN.png' height = '70px'>
**ACGAN**| [Arxiv](https://arxiv.org/abs/1610.09585) | <img src = '/Generative/images/equations/ACGAN.png' height = '70px'>
**EBGAN**| [Arxiv](https://arxiv.org/abs/1609.03126) | <img src = '/Generative/images/equations/EBGAN.png' height = '70px'>
**BEGAN**| [Arxiv](https://arxiv.org/abs/1703.10717) | <img src = '/Generative/images/equations/BEGAN.png' height = '105px'>

<img src = '/Generative/images/gan/GAN_structure.png' height = '500px'>

## GAN
- **GAN**: I Goodfellow, J Pouget-Abadie, M Mirza, B Xu, D Warde-Farley, S Ozair, A Courville, and Y Bengio. Generative adversarial nets. NIPS'14.
- **DC-GAN**: A Radford, L Metz, and S Chintala. Unsupervised representation learning with deep convolutional generative adversarial networks. In ICLR, 2016.
	- First to use Conv
- **EBGAN**: J Zhao, M Mathieu, Y LeCun. Energy-based Generative Adversarial Network. 2016
- Conditional:
	- **CGAN**: Mirza, M. and Osindero, S. Conditional generative adversarial nets. 2014.
	- A Odena, C Olah, and J Shlens. Conditional image synthesis with auxiliary classifier GANs. ICML'17.
		<img src = '/Generative/images/gan/acgan.png' width = '300'>
	- Takeru Miyato and Masanori Koyama. cGANs with projection discriminator. In ICLR, 2018.
- **BEGAN**: D Berthelot, T Schumm, L Metz. BEGAN: Boundary Equilibrium Generative Adversarial Networks. 2017
	- Auto-encoder as a discriminator as was first proposed in EBGAN
	- Maintain a balance between the generator and discriminator losses: E[LG(z)]=gammaE[L(x)]
		<img src = '/Generative/images/gan/began.png' width = '500'>
- W-GAN:
	- **WGAN**: M Arjovsky, S Chintala and Leon Bottou. Wasserstein GAN. 2017
		- Very good explanation: https://vincentherrmann.github.io/blog/wasserstein/
		- Alex Irpan's blog: https://www.alexirpan.com/2017/02/22/wasserstein-gan.html
		- W-GAN is Earth-Mover-Distance
		- Kantorovich-Rubinstein duality
	- **WGAN-GP**: Gulrajani, I., Ahmed, F., Arjovsky, M., Dumoulin, V., and Courville, A. C. Improved training of Wasserstein gans. NIPS'17.
		- Insight: force penalty w.r.t. input is 1 almost everywhere;
		- Code: https://github.com/igul222/improved_wgan_training
		- **Difficulty** with weight constraint: Capacity underuse; Exploding and vanishing gradients; 
		- sup[E_pr(f(x))-E_pg(f(x))]/K, where f() is K-Lipschitz (f's gradient < K)
			<img src = '/Generative/images/gan/wgan-gp.png' width='500'>
	- Jonas Adler, Sebastian Lunz. Banach Wasserstein GAN. NIPS'18
- Attention, Transformer:
	- **SA-GAN**: H Zhang, I Goodfellow, D Metaxas, and A Odena. Self-attention generative adversarial networks. ICML'19
		- https://github.com/heykeetae/Self-Attention-GAN
		- Main module:
		```python
		def forward(self, z):
		    z = z.view(z.size(0), z.size(1), 1, 1) # (?, 100, 1, 1)
		    # deconv + spectral-norm + ReLU
		    # l1, l2, l3: deconv -> spectral-norm -> BN -> RELU
		    out = self.l1(z) # (?, 512, 4, 4)
		    out = self.l2(out) # (?, 256, 8, 8)
		    out = self.l3(out) # (?, 128, 16, 16)
		    out, p1 = self.attn1(out) # (?, 128, 16, 16)
		    out = self.l4(out) # (?, 64, 32, 32)
		    out, p2 = self.attn2(out) # (?, 64, 32, 32)
		    out = self.last(out) # (?, 3, 64, 64)
			return out, p1, p2
		```
		- Self-Attention module for global message passing:
		```python
		def forward(self, x):
			q = self.query_conv(x).permute(0,2,1) # B X CX(N)
        	k =  self.key_conv(x) # B X C x (*W*H)
        	energy =  torch.bmm(q, k) # transpose check
        	attention = self.softmax(energy) # BX (N) X (N) 
        	v = self.value_conv(x) # B X C X N
        	# skip
        	out = torch.bmm(v, attention.permute(0,2,1))
        	out = self.gamma * out + x
	        return out, attention
		```
		- Discriminator:
		```python
		def forward(self, x):
		    # l1, l2, l3: conv -> spectral-norm -> RELU
		    out = self.l1(x)
		    out = self.l2(out)
		    out = self.l3(out)
		    out,p1 = self.attn1(out)
		    out=self.l4(out)
		    out,p2 = self.attn2(out)
		    out=self.last(out)
		    return out.squeeze(), p1, p2
		```
		- Other tricks: two-timescale update rule (TTUR)
		- Experiments: Inception score: 36.8 -> 52.52; Frechet Inception distance: 27.62 -> 18.65
- **SN-GAN**: T Miyato, T Kataoka, M Koyama, Y Yoshida. Spectral Normalization for Generative Adversarial Networks, ICLR'18
	- https://github.com/pfnet-research/sngan_projection
	- Theory: the importance of Lipschitz continuity in assuring the boundedness of statistics
		<img src = '/Generative/images/gan/sn-gan1.png' width = '500'>
	- Spectral Normalization to assure Lipschitz condition.
		<img src = '/Generative/images/gan/sn-gan2.png' width = '500'>
		<img src = '/Generative/images/gan/sn-gan3.png' width = '500'>
	- Algorithm design: generator remains the same, SN on discriminator;
	```python
	class Discriminator(nn.Module):
	    def __init__(self):
	        super(Discriminator, self).__init__()
	        self.conv1 = SpectralNorm(nn.Conv2d(channels, 64, 3, stride=1, padding=(1,1)))
	        ...
	        self.conv7 = SpectralNorm(nn.Conv2d(256, 512, 3, stride=1, padding=(1,1)))
	        self.fc = SpectralNorm(nn.Linear(w_g * w_g * 512, 1))
	```
	- SN modele: divided W by max spectral norm numerically and reset value;
	```python
	@property
    def W_(self):
        w_mat = self.weight.view(self.weight.size(0), -1)
        sigma, _u = max_singular_value(w_mat, self.u)
        self.u.copy_(_u)
        return self.weight / sigma
    def forward(self, input):
        return F.linear(input, self.W_, self.bias)
	```
- **Infogan**: X Chen, Y Duan, R Houthooft, J Schulman, I Sutskever, and P Abbeel. Infogan: Interpretable representation learning by information maximizing generative adversarial nets. NIPS'16
	- Insight: disentangled context c (continuous or discrete) plus noise in generator
	- Maximize the mutual information I(c;G(z,c)):\
		<img src = '/Generative/images/gan/info-gan1.png' width = '400'>
	- MI could be reformulated as reconstructing c. Intuition: knowing x make context c certain:\
		<img src = '/Generative/images/gan/info-gan2.png' width = '550'>
	- Algorithm modules:
		- **Front-End** FE(x): [Conv - BN - LReLU] x 3, produces a 1024-C feature;
		- Q(c|x): encode x to attributes c, Q shared base-conv with D by FE; three output heads, logits for discrete, mu/var for continuous;
		- **Discriminator** D(x): [Conv + Sigmoid] x 3
		- **Generator** G(x): [Deconv-BN-ReLU] x 
	- Put together: D step optimizes FE and D; G step optimizes Q and G\
		<img src = '/Generative/images/gan/info-gan3.jpg' width = '500'>
- Multi-Scale:
	- **Progressive**: Tero Karras, Timo Aila, Samuli Laine, and Jaakko Lehtinen. Progressive growing of GANs for improved quality, stability, and variation. ICLR 2018.
		- https://zhuanlan.zhihu.com/p/30637133
		- G and D for each scale;\
			<img src = '/Generative/images/gan/pgan1.png' width = '500px'>
		- Upscaling x2 as a residual operation:\	
			<img src = '/Generative/images/gan/pgan2.png' width = '500px'>
- Single image:
	- Assaf Shocher, Nadav Cohen, and Michal Irani. Zero-Shot Super-Resolution using Deep Internal Learning. CVPR'18
	- Assaf Shocher, Shai Bagon, Phillip Isola, and Michal Irani. InGAN: Capturing and Remapping the "DNA" of a Natural Image. ICCV'19
	- Tamar Rott Shaham, Tali Dekel, Tomer Michaeli. SinGAN: Learning a Generative Model From a Single Natural Image. ICCV'19 Marr Prize
		- Multi-scale GAN:\
			<img src = '/Generative/images/gan/sin-gan-1.png' width = '400'>
		- A single scale:\
			<img src = '/Generative/images/gan/sin-gan-2.png' width = '400'>

## Techniques
- T Salimans, I Goodfellow, W Zaremba, V Cheung, A Radford, and X Chen. Improved techniques for training gans. NIPS 2016
	- https://github.com/openai/improved_gan
	- **Perception Score** as evaluation
	- Feature matching: immediate layer of discriminator
	- Minibatch discrimination
	- History averaging
	- One-sided label smoothing: replace 0, 1 with .1, .9; smooth only on positive examples in discriminator;
	- Virtual batch normalization: each example x is normalized based on the statistics collected on a reference batch
- **BigGAN**: A Brock, J Donahue, K Simonyan. Large Scale GAN Training for High Fidelity Natural Image Synthesis, ICLR 2019
	- https://github.com/ajbrock/BigGAN-PyTorch.git
	- SA-GAN network structure (Zhang 2018)
	- G: class-conditional BatchNorm (Dumoulin 2017, de Vries 2017)
	- D: projection (Miyato 2018)
	- 2D + 1G: per iteration
	- Moving average (Karras 2018)
	- Orthogonal Initialization (Saxe 2014)
	- **Truncated Norm** to sample z from: big trick
	- IS: precision; FID: recall

## Analaysis
- Metz, L., Poole, B., Pfau, D., and Sohl-Dickstein, J. Unrolled generative adversarial networks. 2016
- Arora, S., Ge, R., Liang, Y., Ma, T., and Zhang, Y. Generalization and equilibrium in generative adversarial nets (gans). 2017
- Heusel, M., Ramsauer, H., Unterthiner, T., Nessler, B., and Hochreiter, S. GANs Trained by a Two Time-Scale Update Rule Converge to a Local Nash Equilibrium. 2017
- Nagarajan, V. and Kolter, J. Z. Gradient descent GAN optimization is locally stable. 2017
- Arjovsky, M. and Bottou, L. Towards Principled Methods for Training Generative Adversarial Networks. 2017
- Lars Mescheder, Sebastian Nowozin, Andreas Geiger. The Numerics of GANs. NIPS'17
	- https://github.com/LMescheder/TheNumericsOfGANs
	- Insight: a game theory perspective, Simultaneous Gradient Ascent;
	- Consensus Optimization;
- W Fedus, M Rosca, B Lakshminarayanan, A Dai, S Mohamed, and I Goodfellow. Many paths to equilibrium: GANs do not need to decrease a divergence at every step. ICLR'18
	- View: a divergence between the training distribution and the model distribution obtains its minimum value at equilibrium
	- This paper: too restrictive
	- Conclusion 1: Both gradient penalties (GAN-GP and DRAGAN-NS) help when training non-saturating GANs, by making the models more robust to hyperparameters.
	- The non-saturating GAN trained with gradient penalties produces better sample (IS)
	- WGAN-GP models perform best on Color MNIST and CIFAR-10.
- Lars Mescheder, Andreas Geiger, and Sebastian Nowozin. Which training methods for GANs do actually converge? ICML'18.
- A Odena, J Buckman, C Olsson, T B. Brown, C Olah, C Raffel, and I Goodfellow. Is generator conditioning causally related to GAN performance? ICML'18.
	- Follow Pennington et al., 2017 to analyze Jacobian;
	- Jacobian generally becomes ill-conditioned at the beginning of training: a good cluster in which the condition number stays the same or even gradually decreases, and a "bad cluster", in which the condition number continues to grow
	- that the average (with z ∼ p(z)) conditioning of the generator is highly predictive of IS and FID;
	- Propose to use Jacobian loss:\
		<img src = '/Generative/images/gan/causal-gan.png' width = '400'>
- A Convex Duality Framework for GANs. NIPS'18
- Are GANs Created Equal? A Large-Scale Study. NIPS'18

## Unclassified	
- E Denton, S Chintala, A Szlam, and R Fergus. Deep generative image models using a laplacian pyramid of adversarial networks. NIPS'15.
- FAIR:
	- Y. Taigman, A. Polyak, and L. Wolf. Unsupervised cross-domain image generation. In ICLR, 2017.
- OpenAI:
	- T Salimans, H Zhang, A Radford, and D Metaxas. Improving GANs using optimal transport. ICLR'18.
- DeepMind:
	- A Brock, T Lim, J.M. Ritchie, and N Weston. Neural photo editing with introspective adversarial networks. ICLR 2017.
	- M G. Bellemare, I Danihelka, W Dabney, S Mohamed, B Lakshminarayanan, S Hoyer, and R Munos. The Cramer distance as a solution to biased Wasserstein gradients. In arXiv preprint arXiv:1705.10743, 2017.
- **NVIDIA**:
	- **SPADE**: T Park, M Liu, T Wang, J Zhu. Semantic Image Synthesis with Spatially-Adaptive Normalization. CVPR'19
		- Key: different scale and bias for different semantic layer!
		- https://github.com/NVLabs/SPADE	
- X Wei, Z Liu, L Wang, and B Gong. Improving the improved training of Wasserstein GANs. ICLR'18
- Inference:
	- V Dumoulin, I Belghazi, B Poole, A Lamb, M Arjovsky, O Mastropietro, and A Courville. Adversarially learned inference.
- Domain adaptation:
	- Y Ganin and V Lempitsky. Unsupervised domain adaptation by backpropagation. ICML'15
- Others:
	- **LSGAN**: X Mao, Q Li, H Xie, R Y.K. Lau, Z Wang, and S. Paul Smolley. Least Squares Generative Adversarial Networks. 2017
	- **DRAGAN**: N Kodali, J Abernethy, J Hays, Z Kira. On Convergence and Stability of GANs. ICLR'18 rejected.
		- https://github.com/kodalinaveen3/DRAGAN
	- M. Liu and O. Tuzel. Coupled generative adversarial networks. In NIPS, 2016
- Super-resolution:
	- C. Ledig, L. Theis, F. Huszar, J. Caballero, A. Aitken, A. Tejani, J. Totz, Z. Wang, and W. Shi. Photo-realistic single image super-resolution using a generative adversarial network. In CVPR, 2017.
	- C. K. Sønderby, J. Caballero, L. Theis, W. Shi, and F. Huszár. Amortised map inference for image super-resolution. In ICLR, 2017.
- GAN + AE (Reconstruction ability):
	- **PixelGAN**: Alireza Makhzani, Brendan Frey. PixelGAN Autoencoders. 2017
		- q(z|x) and p(z) adversarial loss (encoded latent)
		- Reconstruction loss:\
			<img src = '/Generative/images/gan/pixel-gan.png' height = '100px'>
- Graphical Generative Adversarial Networks. NIPS'18
- Yair Weiss. On GANs and GMMs. NIPS'18

## Multi-Modal (Text, ...)
- Shizhan Zhu, Sanja Fidler, Raquel Urtasun, Dahua Lin, Chen Change Loy. Be Your Own Prada: Fashion Synthesis with Structural Coherence. ICCV'17
	- Problem setup: input image + text; output new image (focus on fashion);\
		<img src = '/Generative/images/gan/prada1.png' width = '400'>
	- Model: two GANS:\
		<img src = '/Generative/images/gan/prada2.png' width = '400'>
- **Attngan**: T. Xu, P. Zhang, Q. Huang, H. Zhang, Z. Gan, X. Huang, and X. He. Attngan: Fine-grained text to image generation with attentional generative adversarial networks. CVPR'18
- Text-Adaptive Generative Adversarial Networks: Manipulating Images with Natural Language. NIPS'18

## Feature Learning
- Donahue, J., Krahenbuhl, P., and Darrell, T. Adversarial feature learning.
- Deepak: Unsupervised Feature Learning by Image Inpainting using GANs, CVPR 2016
	- https://github.com/pathak22/context-encoder

## Variational
- Sebastian Nowozin, Botond Cseke, and Ryota Tomioka. **f-GAN**: Training generative neural samplers using variational divergence minimization. NIPS 2016

## RL, Imitation Learning
- Merel, J., Tassa, Y., Srinivasan, S., Lemmon, J., Wang, Z., Wayne, G., and Heess, N. Learning human behaviors from motion capture by adversarial imitation. arXiv preprint arXiv:1707.02201, 2017.

## Misc
- Louppe, G. and Cranmer, K. Adversarial variational optimization of non-differentiable simulators. arXiv preprint arXiv:1707.07113, 2017.

## Codes
- StarGAN: https://github.com/yunjey/StarGAN