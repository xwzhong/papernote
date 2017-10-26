### Recurrent Neural Network Regularization
#### note:
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;文章提出了使用RNN时进行正则化的dropout改进方法。文章中就为什么这个简单的改进可行说得非常好（第三部分结尾），简而言之：传统的dropout对相邻cell中的连接段（connection）也进行了dropout，从而导致“记忆”的丢失，而作者提出的改进只对cell的输入和输出进行dropout，因此既达到了正则化的要求，又不至于丢失long range学到的内容。
#### comment:
  
* 这篇文章适合RNN入门，不仅因为其改进简单有效，而且TensorFlow也提供了这篇paper的代码。另外，理解文章的关键是在哪里进行dropout，特别是multi-layer的情况；
* 在涉及到长时记忆单元时不要进行dropout，仅对输入或输出部分dropout，这个策略不仅适用RNN，其他深度学习算法一样适合。

#### code: 
* [python](https://github.com/tensorflow/models/blob/master/tutorials/rnn/ptb/ptb_word_lm.py)
* [lua](https://github.com/wojzaremba/lstm)

#### more reading:
[what happen to dropout](https://www.reddit.com/r/MachineLearning/comments/5l3f1c/d_what_happened_to_dropout/)
