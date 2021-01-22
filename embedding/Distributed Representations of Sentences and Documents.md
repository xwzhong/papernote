#### note:
　　基于word2vec理论，文章提出句子/篇章编码的方法，分两种模型：

1. paragraph vector-a distributed memory model。模型分三层，输入层、隐含层和输出层，结构图如下：
![](https://github.com/xwzhong/papernote/blob/master/pic/Distributed%20Representations%20of%20Sentences%20and%20Documents.png)

  + 1.1. 训练阶段：
    + a. 输入层：为paragraph id对应的向量、context前k-1个词的词向量（不像cbow模型，由上下文的词预测中心词，这里是用前k-1个词预测第k个词，同时注意，此处的context由paragraph按窗口大小k切分得来）
    + b. 隐含层：步骤a中的向量取平均或拼接
    + c. 输出层：softmax层，对应输出的label为context第k个词

  + 1.2. inference阶段
    + a. 如果paragraph已经出现在训练语料中，则可直接利用训练好的paragraph id对应的向量
    + b. 如果没有，则需初始化这个向量，在固定词向量相关参数的基础上使用梯度下降更新此处初始化的paragraph向量

2. paragraph vector without ordering-distributed bag of words。模型一样分三层：
  + a. 输入层：paragraph id对应的向量
  + b. 隐含层：步骤a中的向量
  + c. 输出层：softmax层，从context中随机抽取m个词，最大化这m个词出现的概率


#### comment:
1. 该方法思路秉承了word2vec cbow和skip-gram的思想，细节方面还是有些不同，比如“paragraph vector-a distributed memory model”是用“paragraph向量+前k-1个词”预测第k个词
2. 个人对“paragraph vector-a distributed memory model”训练和inference步骤的结合上持有异议，训练过程中，词向量相关的参数是变化的，而inference过程中，其是固定的，这样会造成两个过程的不协调，可能是为了加快inference的预测速度而做的改动，个人提出的一个改进策略是，在train阶段分两部分，一部分会改变词向量的参数，另一部分不会，这样就能和预测过程匹配
3. 缺点：
  + a. 参数多。每个paragraph都有一个向量，假定paragraph数跟vocab大小一致，则整个模型的参数量增加一倍，直接拉低训练速度，而往往训练数据的量都比较大，特别是对于短句，动辄上亿，对于长文本，例如新闻，一般也有上百万
  + b. 预测速度慢。预测过程中，如果paragraph不在训练语料中（对于长文本，往往都是不在其训练语料中，如新闻），则需要初始化该paragraph向量，再用梯度下降方式更新其向量，长文本还可得到更多context，每个context都得进行一次或多次梯度更新，非常不友好
4. 这个模型在2016年11月份左右听同事试验过（反馈说用gensim训练速度慢-一方面是没有c加速，word2vec则有），到目前为止在其它论文的对比实验中，很少提到该模型（一两次）
