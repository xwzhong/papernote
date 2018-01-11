#### note:
&emsp;&emsp;该论文对deep learning表现优异的原因进行了实验,思考,在实验的基础上提出了一些观点,虽然有些方面缺乏理论证明,但仍能从其思辨角度了解deep learning的特点.部分要点记录如下:
  1. Randomization tests: Deep neural networks easily fit random labels. 对于random label的训练数据,其训练样本是固定的, 虽然模型train error能达到0%,但是模型学习的是固定下来的label,不是学到random这个过程,如果是学到random这个过程,那么训练好的模型准确率将与random的结果相近;
     + a. The effective capacity of neural networks is sufficient for memorizing the entire data set.
     + b. Even optimization on random labels remains easy. In fact, training time increases only by
a small constant factor compared with training on the true labels.
     + c. Randomizing labels is solely a data transformation, leaving all other properties of the learning problem unchanged.
  2. The role of explicit regularization: Explicit regularization may improve generalization performance, but is neither necessary nor by itself sufficient for controlling generalization error.
  3. Finite sample expressivity: a very simple two-layer ReLU network with p = 2n+d parameters that can express any labeling of any sample of size n in d dimensions.此方面的论证, 可参见Duda的"pattern classification"书籍神经网络部分;
  4. The role of implicit regularization: the algorithm itself is implicitly regularizing the solution. 深度学习模型本身具有泛华能力.个人观点是, SGD本身的拟合方向与数据的特征有一定的交集.

#### comment:
  1. This phenomenon is qualitatively unaffected by explicit regularization, and occurs even if we replace the true images by completely unstructured random noise.此处指, 模型本身的框架是核心,外在的正则化策略(eg: weight decay, dropout等)不能根本上影响深度学习模型的效果;
  2. We corroborate these experimental findings with a theoretical construction showing that simple depth two neural networks already have perfect finite sample expressivity as soon as the number of parameters exceeds the number of data points as it usually does in practice. 此处,如果数据含有明显的规则,那相对的学习时间,参数个数也可减少,更深一步讲,如果模型本身的优化思路跟数据特点切合,那么所需训练数据量,训练时间,参数等可更少;
  3. 少量的噪音能降低模型过拟合的倾向,但噪音越多,其收敛速度也会下降,而且过多的噪音也会严重降低最终的准确率;
  4. paper给人一个非常震撼的观点,指出deep learning更多是以其"记忆"而表现优异, 通过反思自己使用deep learning模型的过程,比较赞同这个观点,DL依旧是基于统计学的方法,只不过其表达能力比传统的机器学习方法更优秀,对于构造通用型人工智能,DL可能只实现其中部分.并不是否定其在某些领域,如图像,语音识别等的惊人表现;
  5. 文章虽然没有给出针对某个领域实质性的改进思路,但是其对深度学习模型的见解对个人了解DL的技术限度有非常大的好处.

#### question:
&emsp;&emsp;为什么random label更难收敛(见fig1 a)? random label数据其样本特征相对正确label更杂乱,规则更不明显,增加了模型训练成本.

#### more reading:
  1. [如何评价 ICLR 2017 中关于 Rethinking Generalization 的那篇文章？](https://www.zhihu.com/question/56151007)
  2. [论文分享：Understanding Deep Learning Requires Rethinking Generalization](https://zhuanlan.zhihu.com/p/26567289)
  3. [论文笔记 understanding deep learning requires rethinking generalization](http://blog.csdn.net/u014380165/article/details/71188924)
  4. [打响新年第一炮，Gary Marcus提出对深度学习的系统性批判](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650735630&idx=1&sn=5840c3e9bed487da3a9080d482fcc58e&scene=21#wechat_redirect)
