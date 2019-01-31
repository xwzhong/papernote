#### note:
&nbsp;&nbsp;&nbsp;&nbsp;文章提出了词向量维度确定的方法，首先指出词向量需满足unitary不变性的特点：无论是词向量夹角（相似性)，还是平行度（类比性），亦或是距离（聚类性），假如把词嵌入整体做一个旋转或者镜面对称，这些几何性质都不会发生变化，而Pairwise Inner Product（PIP）损失能着重测量词嵌入unitary不变性质之间的距离，因此被设计为确定词向量维度的损失函数。

#### comment:
  1. 该策略仍是从词语义分析出发，而不是从后续的高层任务（eg：分类，序列标注等）来确定词嵌入的维度；
  2. paper实验表明，在“词语义”分析上，存在最优词嵌入维度，而且word2vec和glove对过拟合具有鲁棒性，维度非常高时，在词义相似性任务虽有下降，但下降幅度随维度增加并不明显，从这个角度来说，在使用词嵌入的下游任务中是不是也存在最优维度？
  3. [ETH-DS3Lab at SemEval-2018 Task 7](https://github.com/xwzhong/papernote/blob/master/classification/ETH-DS3Lab%20at%20SemEval-2018%20Task%207:%20Effectively%20Combining%20Recurrent%20and%20Convolutional%20Neural%20Networks%20for%20Relation%20Classification%20and%20Extraction.md)为不同词嵌入维度具有不同的效果提供了一个佐证。

#### more:
  1. [NeurIPS 2018 oral论文解读：如何给词嵌入模型选择最优维度](https://www.jiqizhixin.com/articles/2019-01-03-8)
