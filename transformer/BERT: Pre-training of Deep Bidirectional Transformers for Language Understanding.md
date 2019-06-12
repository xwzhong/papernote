#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper在论文"Attention Is All You Need"提出的transformer基础上使用双向编码，并基于“大规模语料”+“两项特定的task”预训练参数，最终在task specific任务中fine tuning，得到论文所有呈现数据集中的最优结果。
  1. bidirectional transformer。[OpenAI GPT](https://blog.openai.com/language-unsupervised/)提出了left-to-right transformer，其仅为单向（every token can only attended to previous tokens in the self-attention layers of the Transformer），同时虽然biLSTM虽然也使用了双向结构，但是这两个方向的LSTM相对独立，paper5.1部分详细实验了去除双向结构的影响。各结构对比详见原文fig1。

  2. pretrain task。数据使用BooksCorpus (800M words) (Zhu et al., 2015) and English Wikipedia (2,500M words)，同时以下面两种task预训练（最终的loss——the sum of the mean masked LM likelihood and mean next sentence prediction likelihood）：

  + Task #1: Masked LM。以15%随机选取句子的中token，同时对于这15%的词——80%用[mask]代替，10%随机选取一个token，10%保留原始的token，对15%token进行细分的原因:
     + a mismatch between pre-training and fine- tuning, since the [MASK] token is never seen dur- ing fine-tuning
     + downside of using an MLM is that only 15% of tokens are predicted in each batch, which suggests that more pre-training steps may be required for the model to converge
  + Task #2: Next Sentence Prediction。由于很多下游任务需要衡量两个句子之间的关系，因此预训练时使用Next Sentence Prediction任务尽量描述这种关系。其中，不同句子部分使用不同的segment embeddings。
  
  3. 实验结果:
  + [GLUE](https://gluebenchmark.com/leaderboard)。11项任务都摘得第一，BERT_large平均score比原最优高6.7;
  + [SQuAD v1.1](https://rajpurkar.github.io/SQuAD-explorer/)。single模型在f1值上超越人类并超过所有其它学者提出的模型；
  + CoNLL-2003 NER。F1 92.6%(原最优)，BERT_large为92.8%;
  + [SWAG](https://leaderboard.allenai.org/swag/submissions/public)。Dev：BERT_base 81.6%；Test：BERT_large 86.3%，openAI GPT 77.97%；human 88%。
  
  4. paper对比了是否使用bidirectional transformer、Next Sentence Prediction等模块，详见5.1，同时发现（5.2），增大模型大小能明显提高各任务的准确率。

#### comment：
  1. 文章可谓NLP领域突破性进展，单一模型能达到如此惊人的效果，其主要得益于双向transformer，大语料特定方式的预训练。强烈推荐看more下reddit讨论部分，上面有原作一些回复；
  2. 训练相同参数下的BERT_large在8 P100s下训练要一年？（详见reddit讨论，注：论文max len为512）；
  3. 针对SWAG数据，它的形式比较像对话系统，将该算法用于闲聊是不是可以有较大的提升（对于多轮编码，可以使用多个segment embeddings）；
  4. pretrain已证明了在各项任务中的优越性，但是针对具体的任务，预训练什么模型结构，用什么样的数据仍需考究。

#### more:
  1. [reddit讨论](https://www.reddit.com/r/MachineLearning/comments/9nfqxz/r_bert_pretraining_of_deep_bidirectional/)
  2. [全面超越人类！Google称霸SQuAD，BERT横扫11大NLP测试](http://www.qianjia.com/html/2018-10/13_307585.html)
  3. [code](https://github.com/google-research/bert)
  4. [深入理解BERT Transformer ，不仅仅是注意力机制](https://www.jiqizhixin.com/articles/2019-03-19-13)
  5. [Bert时代的创新：Bert在NLP各领域的应用进展](https://www.jiqizhixin.com/articles/2019-06-10-7)
  
#### highlight:
  1. We also observed that large data sets (e.g., 100k+ labeled training examples) were far less sensitive to hyperparameter choice than small data sets.
  2. Now you have two representations of each word, one left-to-right and one right-to-left, and you can concatenate them together for your downstream task. But intuitively, it would be much better if we could train a single model that was deeply bidirectional(from reddit讨论).
  3. [SWAG (Situations With Adversarial Generations)](https://leaderboard.allenai.org/swag/submissions/public) is a dataset for studying grounded commonsense inference. It consists of 113k multiple choice questions about grounded situations: each question comes from a video caption, with four answer choices about what might happen next in the scene. The correct answer is the (real) video caption for the next event in the video; the three incorrect answers are adversarially generated and human verified, so as to fool machines but not humans.

