#### note:
　　作者提出在language model中引入已生成word的attention来预测下一个词，大致步骤如下：
  1. 获取当前step之前各个hidden state，并计算各个hidden state的权重，hidden state加权相加后得到当前step的attention c；
  2. 将当前step的hidden state与attention c拼接，最后再进行softmax映射。

#### comment:
  1. 文章提出了两种attention计算方式（式5和式6），设计与seq2seq引入方式相近，扩展来讲，在其它任务中，也能使用类似的attention计算策略；
  2. 根据实验结果来看，该方法对perplexity改进明显（使用了LSTM结构），可分析出，LSTM虽然能学习长序列信息，但是针对LM这个问题仍暴露出其在长序列学习上的不足。
