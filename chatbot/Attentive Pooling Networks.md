### Attentive Pooling Networks

#### note:
&emsp;&emsp;paper是在QA-LSTM/CNN的基础上进行的改进，在介绍QA-LSTM论文中，作者提出了引入单向attention的机制，而在本文中则进行了加强，引入了双向attention，其考虑是基于question和answer能互相影响其生成的vector。

#### comment:
  1. 该paper的亮点在于如何做到question和answer之间相互影响其生成的vector的表达，而原文中的方法有点巧妙，又有点像“杂交”；
  2. 实验结果显示，在insuranceQA test1的结果：QA-LSTM-max66.6%，QA-LSTM attention avg68.1%，AP-LSTM71.7%。

#### highlight:
&emsp;&emsp;In the context of pair-wise ranking or classification with neural networks, AP enables the pooling layer to be aware of the current input pair, in a way that information from the two input items can directly influence the computation of each other's representations.
