### Word or Characters, Fine-grained Gating For Reading Comprehension

#### note:
&emsp;&emsp;paper主要讲了基于word-level和char-level形成high-level vector时的一个改进trick, 该trick是在[miyamoto](https://arxiv.org/abs/1606.01700)基础上提出的，把原来的scalar改为vector。

#### comment:
1. paper提到的改进方案的核心思想是使用能计算的额外知识（如：token的词性，频率等）用模型自动学习的能力把这些知识加到模型中；
2. 在加入这些“知识”的时候，用了gate的思想，有点像LSTM和GRU。

#### practice: 
&emsp;&emsp;目前该方法在SQuAD测试集下的F1为73.327%（Human Performance 91.221%），排名24(2017-06-20)，最新排名见[URL](https://rajpurkar.github.io/SQuAD-explorer/)，微软近期开始致力于从文本中挖掘回复，初步以该数据集为标准，学习reading comprehension可以该网站做参考。
