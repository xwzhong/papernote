#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper提出在训练序列标注模型(BiLSTM+CRF)时，同时进行语言模型训练，要点记录如下：
  + a. loss中加上语言模型的损失；
  + b. 在训练语言模型时，当前token_k仅用正向LSTM输出预测token_k+1，反向LSMT输出预测token_k-1。

#### comment：
  1. 作者提出语言模型想法与[Contextual Bidirectional Long Short-Term Memory Recurrent Neural Network Language Models: A Generative Approach to Sentiment Analysis](https://github.com/xwzhong/papernote/blob/master/neural%20network/Contextual%20Bidirectional%20Long%20Short-Term%20Memory%20Recurrent%20Neural%20Network%20Language%20Models:%20A%20Generative%20Approach%20to%20Sentiment%20Analysis.md)相似，而且都从实验证明的其效果;
  2. [<< Semi-supervised Multitask Learning for Sequence Labeling>>阅读笔记](https://zhuanlan.zhihu.com/p/27899932)文章梳理不错，通读可快速了解文章重点。

#### highlight:
&nbsp;&nbsp;&nbsp;&nbsp;This language modeling objective incentivises the system to learn general purpose patterns of semantic and syntactic composition.
