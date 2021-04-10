#### note:
&nbsp;&nbsp;&nbsp;&nbsp;NER模型可以分为char-based和word-based模型，背景：
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Chinese%20NER%20Using%20Lattice%20LSTM-pic2.png)
  + char-based缺点：char-based模型没有很好地利用词语粒度的信息，char+bichar利用bigram词的embedding信息，char+softword的思想是利用多任务学习共享参数来学习词语粒度的信息
  + word-based缺点：word-based需要首先保证分词的准确率；整合char信息的方式主要是在word embedding时concatenate char语义信息（每个char输入lstm或cnn等到一个向量）
  + 文章提出的模型（lattice lstm）：lattice是基于char-based的NER模型，同时显式地利用了词语粒度信息，利用的地方——在当前字符j的cell vector同时利用了char和word：
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Chinese%20NER%20Using%20Lattice%20LSTM-pic1.png)
    + i. char级别：
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Chinese%20NER%20Using%20Lattice%20LSTM-pic5.png)
    + ii. word级别：
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Chinese%20NER%20Using%20Lattice%20LSTM-pic3.png)
    + iii. 整合char和word：
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Chinese%20NER%20Using%20Lattice%20LSTM-pic4.png)

#### comment:
  1. 文章提出的切入点好，而且引入word的信息相对直接
