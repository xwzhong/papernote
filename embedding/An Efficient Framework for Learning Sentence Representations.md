#### note:
&nbsp;&nbsp;&nbsp;&nbsp;文章提出使用unlabel数据训练句子编码模型，操作很简单，给出一个句子A，预测候选句子(B1,B2,B3...)哪一个是其下一句（分类问题）。

#### comment:
  1. 作者将所提的想法与同样使用unlabel data训练句向量的[skip-thought](https://github.com/xwzhong/papernote/blob/master/sequence%20to%20sequence/Skip-Thought%20Vectors.md)对比，个人认为skip-thought提出时间已经比较早（2015-06，本文提出时间2018-03），skip-thought已经被很多模型超越；
  2. 就为什么文章所提训练策略效果好，作者给出如后解释：Instead of training a model to reconstruct the surface form of the input sentence or its neighbors, we take the following approach. Use the meaning of the current sentence to predict the meanings of adjacent sentences, where meaning is represented by an embedding of the sentence computed from an encoding function。但是仔细一想，说了跟没说差不多，更深层次的原因没法科学论证；
  3. 从实验效果看确实比skip-thought好很多，BERT模型中task2-next sentence prediction跟文章策略有相通之处，但个人认为仍需对第2点所提问题做探索。


#### more:
  1. [tensoflow代码](https://github.com/lajanugen/S2V)
  2. [中文讲解](https://www.jianshu.com/p/50b4094a9c0b)
