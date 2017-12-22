#### note:
&emsp;&emsp;paper提出使用simple RNN语言模型来构建词向量的方法，训练好的模型参数即可转变为词向量，详见式1.

#### comment:
  1. 相比word2vec，RNNLM生成词向量计算量更大，但得到的语法/语义效果更佳，其中一点在于RNNLM考虑了词序；
  2. 在softmax层遇到了与word2vec同样的问题，矩阵维度大导致计算量大（涉及词汇量大小），应该需要进一步的优化，eg：采样；
