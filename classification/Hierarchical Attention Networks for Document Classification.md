#### note:
　　对于文档分类，作者提出从“词->句子->文档”的整体思路构建模型，其中不同“词”和“句子”对当前分类有不同的重要性，因此对此两步采用attention机制进行重要性衡量并提取特征，详见文章fig2。

#### comment:
　　文章提出的观点切合特定场景的问题，特别是对“部分文本内容指向性高”的分类任务中。

#### more:
  1. [一个Hierarchical Attention神经网络的实现](https://blog.csdn.net/triplemeng/article/details/78269127)
  2. [基于Attention机制的深度学习模型在文本分类中的应用](https://www.jianshu.com/p/4fbc4939509f)
  3. [tensorflow code](https://github.com/ilivans/tf-rnn-attention)
  4. [几个模型在dbpedia数据集中的对比](https://github.com/TobiasLee/Text-Classification)
  5. [fasttext在dbpedia数据集的准确率](https://github.com/facebookresearch/fastText/blob/master/docs/supervised-models.md)
