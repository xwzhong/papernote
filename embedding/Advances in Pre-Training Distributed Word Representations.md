#### note:
&emsp;&emsp;paper比较简单,在13年提出的word2vec基础上加了三个近几年提出的改进方案:

  1. Position-dependent Weighting. 原word2vec中,content向量是word vector相加取平均,没有考虑词序影响,position weighting则考虑了词序影响;
  2. Phrase representations. 原始的cbow是基于unigram的,对词序不敏感,在英文中有些词经常同时出现,如: New York. 通过迭代使用mutual information将高度共现的token拼凑到一起,从而改进unigram出现的问题.
  3. [Subword information](https://github.com/xwzhong/papernote/blob/master/embedding/Enriching%20Word%20Vectors%20with%20Subword%20Information.md). 原本的模型结果中,词与词之间的向量没有考虑形态学特征(eg: '太阳'和'阳光','阳'这个字包含的信息在训练好的vector中是不共享的),同时无法解决OOV的问题.

#### comment:
  1. 对于'Phrase representations'用于中文方面,可以直接从分词角度解决;
  2. 句子的词序计算方面,可考虑逆序数,n-gram以及文本提到的Phrase representations;
  3. 文中大部分实验结果是使用fasttext训练得来;
  4. 训练word embeddings时,以句子切分(而不是以段落),同时对句子进行去重,效果会更好(Notably, we have found it very important to de-duplicate sentences in large corpora such as the Common Crawl before training the models);
  5. 实验中,数据比例wiki+news:crawl≈1:31,但使用paper提出的改进,其结果在分类任务中相差不大(avg crawl高0.2%)

#### highlight:
  1. A critical aspect of their training is thus to capture efficiently as much statistical information as possible from rich and vast sources of data.(终究是统计学思路)
  2. We performed the classification using the standard fastText toolkit running in a supervised mode (Joulin et al., 2016), using the pre-trained models to initialize the classifier.
  3. Our findings indicate that improvements can be achieved by training well-known algorithms on very large text datasets, and that using certain tricks can provide further gains in quality.

#### question:
  1. 原word2vec使用paper中的式4进行取样,心存疑惑,为什么不是根据词出现的概率?
  2. [Squad](https://rajpurkar.github.io/SQuAD-explorer/)实验中, 具体是怎么使用embedding的?其指标是使用了EM还是F1score?

#### more reading:
&emsp;&emsp;[论文翻译](http://blog.csdn.net/u014568072/article/details/78940777)
