# Animation

## Physics Based
- ODE, PDE: http://graphics.pixar.com/pbm2001/
- William Reeves: Particle systems— a technique for modeling a class of fuzzy objects, Proc. SIGGRAPH 1983
- Runge-Kutta:
	- Witkin, Baraff, Kass: Physically-based Modeling Course Notes, SIGGRAPH 2001
- Fluid:
	- **SPH** (Smoothed Particle Hydrodynamics)
		- Losasso, F., Talton, J., Kwatra, N. and Fedkiw, R., Two-way Coupled SPH and Particle Level Set Fluid Simulation, IEEE TVCG 14, 797-804 (2008).
	- R. Bridson, J. Hourihan, and M. Nordenstam. Curl noise for procedural fluid flow. SIGGRAPH'07
		- Lennard-Jones force: Repulsive + attractive force;
- Gravity: n-Body problem;
	- **Fast Multipole Method**, Greengard and Rokhlin, J Comput Phys 73, p. 325 (1987)
- http://processing.org/learning/topics/smokeparticlesystem.html

## Unclassified
- **MANN**: He Zhang, Sebastian Starke, Taku Komura, Jun Saito. Mode-Adaptive Neural Networks for Quadruped Motion Control. SIGGRAPH'18
	- Could be used in pedestrian simulation;

## Modeling the skilled movement of articulated figures
- Kinematics:
	- Alla Safonova and Jessica K Hodgins. Construction and optimal search of interpolated motion graphs. TOG'07
	- Yongjoon Lee, Kevin Wampler, Gilbert Bernstein, Jovan Popović, and Zoran Popović. Motion Fields for Interactive Character Locomotion. SIGGRAPH Asia 2010
	- Yuting Ye and C. Karen Liu. 2010b. Synthesis of Responsive Motion Using a Dynamic Model. CGF'10
	- Sergey Levine, Jack M. Wang, Alexis Haraux, Zoran Popović, and Vladlen Koltun. 2012. Continuous Character Control with Low-Dimensional Embeddings. TOG'12
	- Shailen Agrawal and Michiel van de Panne. Task-based Locomotion. TOG'16
	- Daniel Holden, Jun Saito, and Taku Komura. 2016. A Deep Learning Framework for Character Motion Synthesis and Editing. TOG'16
	- Daniel Holden, Taku Komura, and Jun Saito. 2017. Phase-functioned Neural Networks for Character Control. TOG'17
- Physics based: products of an underlying simplified model and an optimization process
	- Stelian Coros, Philippe Beaudoin, and Michiel van de Panne. Generalized Biped Walking Control. TOG'10
	- Yuting Ye and C Karen Liu. Optimal feedback control for character animation using an abstract model. TOG'10
	- Jack M. Wang, Samuel R. Hamner, Scott L. Delp, Vladlen Koltun, and More Specifically. Optimizing locomotion controllers using biologically-based actuators and objectives. TOG'12
	- Igor Mordatch, Emanuel Todorov, and Zoran Popović. Discovery of Complex Behaviors Through Contact-invariant Optimization. TOG'12
	- Yuval Tassa, Tom Erez, and Emanuel Todorov. 2012. Synthesis and stabilization of complex behaviors through online trajectory optimization. IROS'12
	- Shailen Agrawal, Shuo Shen, and Michiel van de Panne. Diverse Motion Variations for Physics-based Character Animation. 2013
	- Kevin Wampler, Zoran Popović, and Jovan Popović. Generalizing Locomotion Style to New Animals with Inverse Optimal Regression. TOG'14
	- Sehoon Ha and C Karen Liu. Iterative training of dynamic skills inspired by human coaching techniques. TOG'14
	- **MPC**: Perttu Hämäläinen, Joose Rajamäki, and C Karen Liu. 2015. Online control of simulated humanoids using particle belief propagation. TOG'15
- RL:
	- Xue Bin Peng, Glen Berseth, and Michiel van de Panne. 2015. Dynamic Terrain Traversal Skills Using Reinforcement Learning. TOG'15
	- Libin Liu and Jessica Hodgins. 2017. Learning to Schedule Control Fragments for Physics-Based Characters Using Deep Q-Learning. TOG'17