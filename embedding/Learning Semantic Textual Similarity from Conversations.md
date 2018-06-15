#### note:
　　文章提出使用对话数据+迁移学习（此处使用了SNLI数据集）来生成句向量，从而用于qa中question rerank，answer rerank和sentence相似度计算等任务中。
  1. 框架整体结构。使用transformer结构（f4-b）对input&response进行编码（fig3），得到两个句向量u和v，再对v使用全连接层映射，得到v'，对u和v'计算score，其中input encoder和response encoder参数相同。
  2. 数据。reddit社区一问多答语料+SNLI文本推理数据。训练中的整合方式时：When training the multitask model, we initialize the shared parameters with a pretrained Reddit model. We employ a distributed training system with multiple workers, where 95% of workers are used to continue training the Reddit task and 5% of workers are used to train the SNLI task。（个人理解在初始化后是同时训练两份数据集）
  3. 实验。设置了多个不同场景的实验：
  
      + a. reddit数据集上response prediction（qa中answer重排）, 结论：相比于DAN(deep averaging network)结构, transformer高8%左右准确率；
      + b. SNLI数据集分类任务。Reddit+SNLI准确率为84.1%；
      + c. STS Benchmark句子相似度（pair有相似得分）。在对原本的cos得分映射后，Reddit+SNLI tuned后test结果为0.808。tuned：For adaptation, the second configuration uses an additional transformation matrix of the sentence embeddings. The matrix is parameterized using the STS training data。（tuned的影响比较大，2%+）；
      + d. CQA Subtask B在qa中对question rerank。

#### comment：
  1. 整一篇文章下来，突出了transformer结构+迁移学习的优点：
  
      + a. transformer结构对比DAN具有明显的优势；
      + b. 使用了SNLI数据使得在STS Benchmark任务中表现突出，但作者也分析了其中的原因（4.4.2），指出：, presumably because most of the SNLI sentences are image captions, while Reddit doesn’t contain much captionstyle data. In contrast, the performance of the models are similar in the other two categories.在CQA Subtask B实验结果中也能得到一定的佐证。进一步讲，在迁移学习中，使用领域相关数据对最终的任务改进才比较明显。
      + c. 文章introduction提到，假设answer相同，则推测其对应question语义相近，但通篇下来似乎没有着重分析；其次，个人认为这是双向的，一句话有多种回复方式，同时一个回复其也可以有多种提问方式，特别是在闲聊领域中，因此一种比较好的方式是结合此两方面的特点。
  2. 引入SNLI分类数据时，作者借鉴了[Conneau et al. (2017)](https://github.com/xwzhong/papernote/blob/master/embedding/Supervised%20Learning%20of%20Universal%20Sentence%20Representations%20from%20Natural%20Language%20Inference%20Data.md)提出的方法：encode a sentence pair into vectors u1, u2 and construct a feature vector (u1, u2, |u1 − u2|, u1 ∗ u2).
  3. 文章摘要中写道：Our method trains an unsupervised model to predict conversational input-response pairs. 此处说unsupervised似乎不太合理，作者只是没有使用人工标注的数据集，而使用了确定的一问一答语料+SNLI语料。
  4. 在句子相似度匹配上，半监督学习或许是不错的思路。首先使用大语料训练一个无监督模型，然后再设计有监督的模型（该模型可能和无监督模型一样，也可能不一样），利用极少的数据微调模型，主要是考虑到有标注数据的缺失，同时利用领域相近的数据一般能学到相似的知识，[Learning to Generate Reviews and Discovering Sentiment](https://github.com/xwzhong/papernote/blob/master/neural%20network/Learning%20to%20Generate%20Reviews%20and%20Discovering%20Sentiment.md)就是一个例子。

#### more:
  1. [Learning Semantic Textual Similarity from Conversations 论文实现](https://blog.csdn.net/sinat_30665603/article/details/80174128)
  2. [如何匹配两段文本的语义？](https://www.jiqizhixin.com/articles/2018-06-11-17)
   
