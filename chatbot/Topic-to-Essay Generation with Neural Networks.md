### Topic-to-Essay Generation with Neural Networks

#### note:
&emsp;&emsp;针对具体任务：给出几个主题词，生成该词下的短文本，文章给出了两个常规方案和一个主题衰减方案：
1. 将主题词的词向量相加求平均，按语言模型方式逐字生成；
2. 在主题词的之上增加一层attention，类似seq2seq方式生成；
3. 在2的基础上，给每一步的各个主题词权重进行加权，减小该主题词已生成时再次出现的概率。结构图如下：

![](https://github.com/xwzhong/papernote/blob/master/pic/Topic-to-Essay_Generation_with_Neural_Networks3.PNG)

#### comment:
1. 文章主要亮点在于主题词权重在生成过程中衰减这块。


#### more reading:
1. [Topic-to-Essay Generation with Neural Networks阅读笔记和部分实验](https://blog.csdn.net/firesolider/article/details/94387427)
2. [IJCAI 2018 基于主题信息的神经网络作文生成模型](https://www.jiqizhixin.com/articles/2018-06-05)
