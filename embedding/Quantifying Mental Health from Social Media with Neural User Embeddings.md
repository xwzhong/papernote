#### note:
&nbsp;&nbsp;&nbsp;&nbsp;文章想根据“用户发的推特”学习用户向量表征，达到以下目的：
  + a. 对于“抑郁症患者”“创伤后应激障碍患者”“对照组（未上述疾病用户）”三类数据，在空间上是否有聚类特点
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Quantifying%20Mental%20Health%20from%20Social%20Media%20with%20Neural%20User%20Embeddings.png)
  + b. 将向量表示用于下游任务
用户向量训练策略：用户index -> user embedding（类似从词转id中的word embedding）-> 计算“用户向量”和“推特中出现的词向量”的dot product -> 使用hinge loss（负样本词为不在推特文本中的词）

#### comment:
  1. 该策略类似[paragraph2vector](Distributed Representations of Sentences and Documents)，固定paragraph/用户向量，但同时也明显存在缺陷，对于没有出现过的用户回出现“OOV”，可以考虑将用户tag当作用户表征，对于直接使用用户唯一标识作为输入的模型都有一定程度的缺陷；
  2. 用于下游任务时，固定用户embedding后加一个全连接层，效果更佳（文章给的解释是提供了提供了领域和任务的特征）

#### more:
  1. [github代码](https://github.com/samiroid/usr2vec)
