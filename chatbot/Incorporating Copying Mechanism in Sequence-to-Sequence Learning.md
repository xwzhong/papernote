### Incorporating Copying Mechanism in Sequence-to-Sequence Learning

#### note:
&emsp;&emsp;针对seq2seq无法生成OOV词但属于encoder中的词情况，作者提出了一种复制encoder词汇的策略，词的分布示意图如下：

![](https://github.com/xwzhong/papernote/blob/master/pic/copyNet_vocab.PNG)

+ 当前step各个词的概率为以下两部分概率分布的和：
  + a. 生成模式得分p(yt, g|·)：按照常规计算方式得到，详见下式：
![](https://github.com/xwzhong/papernote/blob/master/pic/copyNet_generate_mode.PNG)

  + b. 复制模式得分p(yt, c|·)：在encoder中出现的词向量经映射后激活，再乘以隐层，详见下式：
![](https://github.com/xwzhong/papernote/blob/master/pic/copyNet_copy_mode.PNG)

+ 隐层状态的更新：常规做法是根据一个隐层状态和输出y_t-1，以及attention c，copyNet在y_t-1路径新增了复制机制，词y_t-1的表示为其本身的向量和encoder输出加权并拼接的结果，详见下列公式：
![](https://github.com/xwzhong/papernote/blob/master/pic/copyNet_state.PNG)

模型结构图如下：
![](https://github.com/xwzhong/papernote/blob/master/pic/copyNet_model.PNG)

#### comment:
1. copyNet在encoder-decoder模型任务中，如果decoder的文本大部分出现在encoder中（比如：文本摘要，抽取式生成），该模型的效果会表现比较好；
2. copy模式在decoder输出部分各个词的概率分布部分计算巧妙。

#### more reading:
1. [CopyNet解读](https://blog.csdn.net/xvshiting/article/details/82216112)
