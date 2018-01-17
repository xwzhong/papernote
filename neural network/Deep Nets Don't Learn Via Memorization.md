#### note:
&emsp;&emsp;论文主要是反驳[Understanding Deep Learning Requires Rethinking Generalization](https://arxiv.org/abs/1611.03530)提出的观点, 在摘要部分已将文章思想讲得很清楚: We use empirical methods to argue that deep neural networks (DNNs) do not achieve their performance by memorizing training data, in spite of overlyexpressive model architectures. Instead, they learn a simple available hypothesis that fits the finite data samples, In support of this view, we establish that there are
qualitative differences when learning noise vs. natural datasets, showing that:
  1. more capacity is needed to fit noise;
  2. time to convergence is longer for random labels, but shorter for random inputs;
  3. DNNs trained on real data examples learn simpler functions than when trained with noise data, as measured by the sharpness of the loss function at convergence;
  最后作者也指出: for appropriately tuned explicit regularization, e.g. dropout, we can degrade DNN training performance on noise datasets without compromising generalization on real data.

#### comment:
  1. 针对本文提到的几个观点,个人对此实验现象理解如下:
     + a. noise data内在的模式比正常标注的数据模式更简单(eg:区分男人/女人比区分不同种族更容易), 因此拟合noise数据需要更多的参数及相应的计算;
     + b. random label并没有改变输入变量x的模式(pattern),该模型相比对input数据加入噪声更规整,导致从特征到标签的学习难度加大(输入是规整,输出是random);而对input加入噪声,其内部模式发生了变化,因此output对random后的input也是random的(它不需要知道output有什么样的模式,因为output是由input推导而来),所以相比random label更易拟合;在此猜测,如果同时对input和output进行random操作,其拟合速度与仅对input进行random操作接近;
     + c. real data有更简洁的pattern因此需要更少的参数及训练时间;
  2. 个人觉得本文提出的反驳意见与rethinking generalization提出的观点不冲突:
     + a. rethinking generalization这篇论文侧重表达DL的拟合能力强,哪怕对input数据随机加入噪声,但只要参数足够大,训练时间足够长,training accuracy都能达到百分百;
     + b. 本文侧重说明dl不是单纯具有数据的'记忆'能力,从real data和noise data看出, 其本身也具有很强的泛化能力.该观点在rethinking那篇论文中也有提及.
  3. 同一个模型,hidden unit越大,收敛速度越快(fig2).

#### question:
&emsp;&emsp;在2.3部分-effect of regularization on learning, 除了说明不同正则化方法在noise data下的不同表现还说明了说明?

#### more reading:
  1. [论文笔记:Understanding Deep Learning Requires Rethinking Generalization](https://github.com/xwzhong/papernote/blob/master/neural%20network/Understanding%20Deep%20Learning%20Requires%20Rethinking%20Generalization.md)
  2. [讨论](https://openreview.net/forum?id=rJv6ZgHYg)
