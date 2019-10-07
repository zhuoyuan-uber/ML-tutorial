# CNN for 3D Data

## Point Clouds
- **Grid-Cell**:
	- **PointGrid**: T. Le and Y. Duan. PointGrid: A deep network for 3D shape understanding. CVPR 2018
		- Preprocessing: normalize to [-1, 1]
		- Each grid cell: **exactly K=4 points** in 16 x 16 x 16, each cell 3K-dim feature; if originally >= K points, sample; < K, sample with replacement
		<img src="/CV-3D/images/cnn_3d/pointgrid.png" alt="drawing" width="600"/>
	
	- **SplatNet**: H. Su, V. Jampani, D. Sun, S. Maji, E. Kalogerakis, M.-H. Yang, and J. Kautz. SplatNet: Sparse lattice networks for point cloud processing. CVPR'18
		- Input: point clouds and images; output semantic for each point;
		- BCL (Bilateral Convolution Layer): 1. Splat: project onto lattice; 2. Convolve; 3. Slice. Can have different scale size;
		- 2D-3D: DeepLab segmentation for 2D images/rendered from mesh; project pixels to 3D, BCL;
		<img src="/CV-3D/images/cnn_3d/splatnet1.png" alt="drawing" width="450"/>
		<img src="/CV-3D/images/cnn_3d/splatnet2.png" alt="drawing" width="600"/>
		<img src="/CV-3D/images/cnn_3d/splatnet3.png" alt="drawing" width="600"/>

	- **Kd-network**: R. Klokov and V. Lempitsky. Escape from cells: Deep Kd-networks for the recognition of 3D point cloud models. ICCV'17
		- Irregular grid;
		- http://sites.skoltech.ru/compvision/kdnets/
		- Construction: Work with Kd-tree; (top-down, every node split the axis with largest span);
		- Non-leaf nodes: Recursive bottom-up, Recursive-NN;
		- Properties: Layerwise parameter sharing; Hierarchical representation; Partial invariance to jitter; Non-invariance to rotations; Role of kd-tree structure;
		- Experiments: MNIST 2D points; ModelNet;
		<img src="/CV-3D/images/cnn_3d/kd-network1.png" alt="drawing" width="500"/>
		<img src="/CV-3D/images/cnn_3d/kd-network2.png" alt="drawing" width="400"/>
		<img src="/CV-3D/images/cnn_3d/kd-network3.png" alt="drawing" width="500"/>

- **Unordered**:
	- **PointNet**: H Su, C Qi, K Mo, L Guibas. PointNet: Deep Learning on Point Sets for 3D Classification and Segmentation, CVPR'17
		<img src="/CV-3D/images/cnn_3d/pointnet.png" alt="drawing" width="600"/>

	- **PointNet++**:  Charles R. Qi, Li Yi, Hao Su, Leonidas J. Guibas. Deep Hierarchical Feature Learning on Point Sets in a Metric Space, NIPS'17
		- **Classification mode**: [SA module x 3] + FC_layers;
		- **Semantic Segmentation mode**: [SA-module x3] + [FP-modules x4] + [Conv1d x2]
		- SA module #1, #2: xyz, features = model(xyz, features=None), xyz: (B, 2048, 3)
			- Gather operation: **FPS** (furtherest point sampling), from N points, select N' < N centers as new_xyz (B, N', 3)
			- Group-Query-MLP x 3 (with different radius)
				- Group and Query: to (B, d, N', nS), dim: feature dim; each N' centers will be assigned nS=16 members
				- Shared MLPs: with dim like [d, 32, 32, 64], output (B, 64, N', nS), implement FC with 2D-Conv with kernel-size (1, 64)
				- Max-pooling along last dimension (B, 64, 512)
			- After SA-1: xyz=(B, 512, 3), feat=(B, 320, 512)
			- After SA-2: xyz=(B, 128, 3), feat=(B, 640, 128)
		- SA module #3:
			- No gather operation: new_xyz=None
			- GroupAll: (B, 643, 1, nS), 643=640+3, nS=128
			- Shared MLPs: (B, 1024, 1)
		- FC_layers: [1024, 512, 256, nClass]
		- Finally a 256-dim feature
		- FPN-modules are used to **interpolate features back**;
		```python
		feat[i-1] = self.FP_modules[i](xyz[i-1], xyz[i], feat[i-1], feat[i])
		```	
		- With shape: (B, n, 3), (B, m, 3), (B, C1, n), (B, C2, m), returns (B, mlp[-1], n)
		<img src="/CV-3D/images/cnn_3d/pointnet++.png" alt="drawing" width="600"/>

	- **Frustum PointNet**: C Qi, W Liu, C Wu, H Su, L Guibas. Frustum PointNets for 3D Object Detection from RGB-D Data, CVPR'18
		- RGB-D
		- 2D-detection: 2D bounding boxes;
		- 3D-frustum: FPN; pointnet classification for each point; T-net (STN)
		<img src="/CV-3D/images/cnn_3d/frustum-pointnet.png" alt="drawing" width="600"/>
	- **Foldingnet**: Y. Yang, C. Feng, Y. Shen, and D. Tian. Foldingnet: Interpretable unsupervised learning on 3d point clouds. arXiv'17.
	- P. Achlioptas, O. Diamanti, I. Mitliagkas, and L. Guibas. Learning representations and generative models for 3d point clouds. 2018.

- **Attention**:
	- **3D-Transformer**: S Xie, S Liu, Z Chen, Z Tu. Attentional ShapeContextNet for Point Cloud Recognition. CVPR'18
		- Feature of point pi: Histogram of pj-pi (24 bins = 3 radius x 8 angle)
		<img src="/CV-3D/images/cnn_3d/3d-transformer.png" alt="drawing" width="600"/>

- P. Hermosilla, T. Ritschel, P.-P. Vazquez, A. Vinacua, and T. Ropinski. Monte carlo convolution for learning on non-uniformly sampled point clouds. TOG'18
	- Point Clouds (generally non-uniform);
	- Estimate sample density distribution;
	- https://github.com/viscom-ulm/MCCNN
- J. Li, B. M. Chen, and G. H. Lee. SO-Net: Self-organizing network for point cloud analysis. CVPR'18
- Y. Li, R. Bu, M. Sun, and B. Chen. PointCNN: Convolution on X-transformed points. NIPS'18
	- 1 weighting: of the input features associated with the points, 
	- 2.permutation: into a latent and potentially canonical order
	- https://github.com/yangyanli/PointCNN
	<img src="/CV-3D/images/cnn_3d/pointcnn1.png" alt="drawing" width="600"/>
	<img src="/CV-3D/images/cnn_3d/pointcnn2.png" alt="drawing" width="600"/>

- **DGCNN**: Y Wang, Y Sun, Z Liu, S Sarma, M Bronstein, and J Solomon. Dynamic Graph CNN for Learning on Point Clouds. 2018

## Voxel
- B. Graham, M. Engelcke, and L. van der Maaten. 3D semantic segmentation with submanifold sparse convolutional networks. CVPR 2018
	- SSCN (submanifold sparse Conv Net)
	- https://github.com/facebookresearch/SparseConvNet
	- SSCN(m, n, f, s): m input, n output, f filter-size, s stride;
	- Implementation: a hash table (https://github.com/sparsehash/sparsehash) and a matrix;
	- **Sparse Voxelized**: applied on Submanifold FCN and U-Nets;
	- CPU-only;
	- Experiments: ShapeNet; NYU depth;
- Oct-tree:
	- **OGN**: M. Tatarchenko, A. Dosovitskiy, and T. Brox. Octree generating networks: Efficient convolutional architectures for high-resolution 3d outputs. ICCV'17

## Mesh
- J. Bruna, W. Zaremba, A. Szlam, and Y. LeCun. Spectral networks and locally connected networks on graphs. 2013
- A. Sinha, J. Bai, and K. Ramani. Deep learning 3d shape surfaces using geometry images. ECCV'16
- M. Defferrard, X. Bresson, and P. Vandergheynst. Convolu- tional neural networks on graphs with fast localized spectral filtering. NIPS'16 
- T. Bagautdinov, C. Wu, J. Saragih, P. Fua, and Y. Sheikh. Modeling facial geometry using compositional vaes.
- O. Litany, A. Bronstein, M. Bronstein, and A. Makadia. Deformable shape completion with graph convolutional autoencoders. CVPR'17.
- N. Verma, E. Boyer, and J. Verbeek. Feastnet: Feature- steered graph convolutions for 3d shape analysis
- H. Maron, M. Galun, N. Aigerman, M. Trope, N. Dym, E. Yumer, V. G. Kim, and Y. Lipman. Convolutional neural networks on surfaces via seamless toric covers. 2017.
- P. Baque, E. Remelli, F. Fleuret, and P. Fua. Geodesic convolutional shape optimization. 2018
- **AtlasNet**. T. Groueix, M. Fisher, V. G. Kim, B. C. Russell, and M. Aubry. Atlasnet: A papier-mache approach to learning 3d surface generation. CVPR'18
- H. B. Hamu, H. Maron, I. Kezurer, G. Avineri, and Y. Lipman. Multi-chart generative surface modeling. 2018
- Legacy:
	- **Marching cubes**: W. E. Lorensen and H. E. Cline. Marching cubes: A high resolution 3d surface construction algorithm. SIGGRAPH'87
	- M. Tarini, K. Hormann, P. Cignoni, and C. Montani. Polycube-maps. TOG'04

## SDF
- Legacy:
	- B. Curless and M. Levoy. A volumetric method for building complex models from range images. SIGGRAPH'96
	- **Kinectfusion**: R. A. Newcombe, S. Izadi, O. Hilliges, D. Molyneaux, D. Kim, A. J. Davison, P. Kohi, J. Shotton, S. Hodges, and A. Fitzgibbon. Kinectfusion: Real-time dense surface mapping and tracking. ISMAR'11
- Voxel-based SDF
	- A. Zeng, S. Song, M. Nießner, M. Fisher, J. Xiao, and T. Funkhouser. 3dmatch: Learning local geometric descriptors from rgb-d reconstructions. CVPR'17
	- **3D-EPN**: A. Dai, C. R. Qi, and M. Nießner,  Shape completion using 3d-encoder-predictor cnns and shape synthesis, CVPR'17
		- https://github.com/angeladai/cnncomplete
	- D. Stutz and A. Geiger. Learning 3d shape completion from laser scan data with weak supervision. CVPR'18
- Point SDF:
	- **DeepSDF**: J Park, P Florence, J Straub, R Newcombe, S Lovegrove. DeepSDF: Learning Continuous Signed Distance Functions for Shape Representation. 2019

## 2D-3D Fusion
- V. Hegde and R. Zadeh. FusionNet: 3D object classification using multiple data representations. 2016