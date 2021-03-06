# Language Modeling

## Benchmark
- https://gluebenchmark.com/leaderboard/

## Semi-supervised (SOA)
- Legacy:
	- R Collobert and J Weston. A unified architecture for natural language processing: Deep neural networks with multitask learning. ICML'08
	- Mikolov, T.; Karafit, M.; Burget, L.; Cernock, J.; and Khudanpur, S. 2010. Recurrent neural network based language model. INTERSPEECH 2010
	- R Collobert, J Weston, L Bottou, M Karlen, K Kavukcuoglu, and P Kuksa. Natural language processing (almost) from scratch. JMLR'11
	- Mikolov, T.; Kombrink, S.; Burget, L.; ernock, J.; and Khudanpur, S. 2011. Extensions of recurrent neural network language model. ICASSP 2011
	- Sundermeyer, M.; Schluter, R.; and Ney, H. Lstm neural networks for language modeling. 2012
- **ELMO**: Matthew E. Peters, Mark Neumann, Mohit Iyyer, Matt Gardner, Christopher Clark, Kenton Lee, Luke Zettlemoyer. Deep contextualized word representations. NAACL‘18
	- https://allennlp.org/elmo
	- ELMo (Embeddings from Language Models)
	- bidirectional LSTM, predict next/last word
- **Attention**: D Bahdanau, K Cho, and Y Bengio. Neural machine translation by jointly learning to align and translate. arxiv'14
- Transformer/BERT series:
	- **GMNT**: Y. Wu, M. Schuster, Z. Chen, Q.V. Le, M. Norouzi, et al. Google's Neural Machine Translation System: Bridging the Gap between Human and Machine Translation. 2016
		<img src="/NLP/images/gmnt.png" alt="drawing" width="500"/>

		- WordPiece for Korean, Japanese
		<img src="/NLP/images/gmnt2.png" alt="drawing" width="500"/>
	- **Transformer**: Attention is all you need. NIPS 2017
		- A very good intro: http://jalammar.github.io/illustrated-transformer/
		- Explanation with Pytorch: http://nlp.seas.harvard.edu/2018/04/03/attention.html
		- https://github.com/Kyubyong/transformer
		- Pytorch: https://github.com/jadore801120/attention-is-all-you-need-pytorch
		<img src="/NLP/images/transformer1.png" alt="drawing" width="500"/>
		<img src="/NLP/images/transformer2.png" alt="drawing" width="600"/>
	- **BERT**: Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova. BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding. ACL'19
		- **Bidirectional Transformer** as model (L=12 for Base, L=24 for Large);
		- **Embedding**: sum of following three;
			- **WorldPiece** (Wu et al 2016): 30,000 tokens;
			- Learned positional embedding;
			- Segment embedding; (same sentence share same emb?)
		- Pretrain tasks:
			- Masked LM (15%): in the 15%, 10% replaced with other words, 10% unchanged, 80% [MASK]. So the model has to attend to every word.
			- Given two sentences concatenated together. Predict if B is next to A (50%). Achieve 97-98% accuracy;
		- Pretrain:
			- BooksCorpus (800M) + Wiki (2,500M), 1 Billion only sentence level;
			- BERT-BASE: 4 Cloud TPUs (16 chips), 4 days;
			- BERT-LARGE: 4 Cloud TPUs (64 chips), 4 days;
		- Fine-tunning:
			- First token [CLS], finally used as classifier after FC and softmax;
		<img src = '/Weak-Unsupervised/images/bert.png' width = '600px'>
	- Neil Houlsby, Andrei Giurgiu, Stanislaw Jastrzebski, Bruna Morrone, Quentin de Laroussilhe, Andrea Gesmundo, Mona Attariyan, Sylvain Gelly. Parameter-Efficient Transfer Learning for NLP. ICML'19
		- Adapter module
	- Y You, J Li, J Hseu, X Song, J Demmel, C Hsieh. Reducing BERT Pre-Training Time from 3 Days to 76 Minutes. 2019
		- Batch-size: 64k - 32k
		- Optimizer: **LAMB** (Layer-wise Adaptive Moments optimizer for Batch training)
		- Iteration: 1m -> 8,599
	- **Transformer-XL**: Z Dai, Z Yang, Y Yang, J Carbonell, Q Le, R Salakhutdinov. Transformer-XL: Attentive Language Models Beyond a Fixed-Length Context. 2019
		- https://github.com/kimiyoung/transformer-xl
		- Fixed-length segment;
		- Improved on Rami Al-Rfou et.al. 2018 [Character-level language modeling with deeper self-attention]
		- Cached previous hidden states;
	- **XLNet**: Zhilin Yang, Zihang Dai, Yiming Yang, Jaime Carbonell, Ruslan Salakhutdinov, Quoc V. Le. XLNet: Generalized Autoregressive Pretraining for Language Understanding. 2019
		- https://github.com/zihangdai/xlnet
- OpenAI GPT Series:
	- **GPT**: A Radford, K Narasimhan, T Salimans, I Sutskever. Improving Language Understanding by Generative Pre-Training. 2018
		- https://github.com/openai/finetune-transformer-lm
		- Causal Transformer;
		- Semi-supervised fine-tuning;
		- Pretrain: BooksCorpus dataset;
		- 12 x self-attention (Transformer);
	- R Al-Rfou, D Choe, N Constant, M Guo, L Jones. Character-Level Language Modeling with Deeper Self-Attention. 2018
		- 64 transformer layers (deep, multi-head self-attention + fc x 2);
		- Mask for causal attention;
		- Auxiliary loss:
			- Multiple prediction (predict every character in the sequence)
			- Intermediate layer losses (deep supervision)
			- Multiple targets
		- 235 million parameters, dropout (0.55)
	- **GPT-2**: A Radford, J Wu, R Child, D Luan, D Amodei, I Sutskever. Language Models are Unsupervised Multitask Learners. 2018
		- Input representation: Byte Pair Encoding (BPE) (Sennrich et al., 2015); A Character-Level Decoder without Explicit Segmentation for Neural Machine Translation (Yoshua Bengio)
		- Layer normalization: moved to the input of each sub-block
		- additional layer normalization: after the final self attention block
		- 48 layers of transformer
	- R Child, S Gray, A Radford, and I Sutskever. Generating long sequences with sparse transformers. 2019
- G Lample and A Conneau. Cross-lingual language model pretraining. 2019
- C Wang, M Li, A J. Smola. Language Models with Transformers. 2019
	<img src="/NLP/images/candidate-sample.png" alt="drawing" width="500"/>
	<img src="/NLP/images/coordinate-as.png" alt="drawing" width="600"/>
- NVIDIA:
	- Megatron: https://github.com/NVIDIA/Megatron-LM

## Character Level
- **BPE**: 
	- Rico Sennrich, Barry Haddow, and Alexandra Birch. Neural machine translation of rare words with subword units. 2015
	- FastBPE: https://github.com/glample/fastBPE

## Generation
- Controlled Generation:
	- **CTRL**: N Keskar, B McCann, L Varshney, C Xiong, R Socher. CTRL: A Conditional Transformer Language Model for Controllable Generation. 2019
		- Insight: **conditional Transformer**; control code as first word without special treatment;
		- https://github.com/salesforce/ctrl
		- fastBPE for subword
		- No PAD, MASK, ...
		- Tied embeddings with vocabulary size 250k
		- 48-layer transformer; 1.63B parameters
		- Sampling with temperature;
		- Control codes: style by domain; more complex; specific task; zero-shot code-mixing;
		- Trained on 256 core of TPU v3; 800k iterations with AdaGrad; batch-size=1024;
	- Finetune with RL: Daniel M. Ziegler, Nisan Stiennon, Jeffrey Wu, Tom B. Brown, Alec Radford, Dario Amodei, Paul Christiano, and Geoffrey Irving. Fine-tuning language models from human preferences. arXiv'19
	- Training with conditions:
		- Yuta Kikuchi, Graham Neubig, Ryohei Sasano, Hiroya Takamura, and Manabu Okumura. Controlling output length in neural encoder-decoders. EMNLP'16
		- Jessica Ficler and Yoav Goldberg. Controlling linguistic style aspects in neural language generation. 2017
	- **SeqGAN**: L Yu, W Zhang, J Wang, and Y Yu. SeqGAN: Sequence generative adversarial nets with policy gradient. AAAI'17
	- **PPLM**: Sumanth Dathathri, Andrea Madotto, Janice Lan, Jane Hung, Eric Frank, Piero Molino, Jason Yosinski, Rosanne Liu. Plug and Play Language Models: a Simple Approach to Controlled Text Generation. ICLR'20
		- https://github.com/uber-research/pplm
		- Insight: modify history in the direction to maximize both p(x) and p(a|x), then we get p(x|a);
			<img src="/NLP/images/pplm.png" alt="drawing" width="400"/>
- Steer (with a small NN?):
	- Jiatao Gu, Graham Neubig, Kyunghyun Cho, and Victor OK Li. Learning to translate in real-time with neural machine translation. arxiv'16
	- Jiatao Gu, Kyunghyun Cho, and Victor OK Li. Trainable greedy decoding for neural machine translation. arxiv'17
	- Yun Chen, Victor OK Li, Kyunghyun Cho, and Samuel R Bowman. A stable and effective learning strategy for trainable greedy decoding. arxiv'18
	- Nishant Subramani, Sam Bowman, and Kyunghyun Cho. Can unconditional language models recover arbitrary sentences? arxiv'19
- Ari Holtzman, Jan Buys, Maxwell Forbes, Antoine Bosselut, David Golub, and Yejin Choi. Learning to write with cooperative discriminators. CoRR'18
