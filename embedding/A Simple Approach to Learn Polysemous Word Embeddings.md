### A Simple Approach to Learn Polysemous Word Embeddings

#### note:
&emsp;&emsp;paper提出一种解决word embedding在一词多义的表示问题.原理比较简单,给定pretrained词向量(eg: word2vec, glove等),并计算词汇表中两两之间的cooccurance(paper式1),最后,指定词的word embedding由当前context下所有词的加权embedding.

#### comment:
  1. paper提出的方法简单,换一个思路理解,就是利用了当前context的信息来确定该词的表示;
  2. 虽然使用了context文本信息,但仍是一种统计特征;
  3. 在experiment中,不同测试集的结果相对其它模型差异大.

#### [code](https://github.com/dingwc/multisense)

#### highlight:
&emsp;&emsp;We note that (Chen et al., 2014) is learned using additional supervision from the WordNet knowledge-base in clustering; therefore, it achieves comparably much higher scores in WSR and CWS tasks in which the evaluation is also based on WordNet.
