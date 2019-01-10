#### note:
&nbsp;&nbsp;&nbsp;&nbsp;针对有监督任务中数据量少的情况，作者提出使用半监督的方式强化句子层面的表示。以下图为例：

![](https://github.com/xwzhong/papernote/blob/master/pic/Semi-Supervised%20Sequence%20Modeling%20with%20Cross-View%20Training.png)
  
  + a. 有标签任务中需要预测Washington为地点；
  + b. 在无标签的任务中，仅提取句子部分信息，同样需要预测'Washington'为地点。此处，'Washington'可能不可见，预测时，最后一层softmax层参数不同，其余相同，监督方式为使用KL散度拟合与步骤a的输出分布。


#### comment:
&nbsp;&nbsp;&nbsp;&nbsp;文章主要的想法是深化句子层面的语义表征，跟近期的BERT有相通之处，但使用的数据量相对于BERT少很多。


#### more:
  1. [tensoflow代码](https://github.com/tensorflow/models/tree/master/research/cvt_text)
  2. [遗珠之作？谷歌Quoc Le这篇NLP预训练模型论文值得一看](https://www.jiqizhixin.com/articles/2019-01-07-5)
