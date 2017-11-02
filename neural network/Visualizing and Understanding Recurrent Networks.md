#### note:
&emsp;&emsp;paper通过实验对语言模型的一些特点进行了定量分析。分析的方面有：
  1. RNN、GRU和LSTM的对比；
  2. LSTM hidden unit与句子长度的定量关系；
  3. 结合fig1和tab2可估算不同参数的RNN变体与n-gram、n-NN模型表达能力的关系等。

#### comment:
  1. 在language model中，RNN增加layer层数进行对比，可从参数总量不变的条件下去看（eg：1layer-128size VS 2layer-64size对比），可发现RNN、GRU和LSTM在1layer的情况下，效果往往更好；
  2. RNN记忆文本的长度与参数和文本使用该模型学习难易相关。往往参数越大，学习能力自然越强；同时，如果所选模型切合待训练数据，其学习的效果自然更佳；
  3. 文中提到一个“interpretable lsmt cell”，其与[论文](http://de.arxiv.org/pdf/1704.01444)提到的sentiment unit相像，详细分析可见[笔记](https://github.com/xwzhong/papernote/blob/master/neural%20network/Learning%20to%20Generate%20Reviews%20and%20Discovering%20Sentiment.md)；
  4. 从论文的分析可了解到，RNN、GRU和LSTM仍像统计模型。
