### curriculum learning

#### note:
&emsp;&emsp;paper提出的curriculum learning有点类似人类学习机制——先学简单的技能，再学困难的。用作者的话说：The basic idea is to start small, learn easier aspects of the task or easier subtasks, and then gradually increase the difficulty level。该trick在运用过程中，仅需改变训练数据集中不同sample的训练数据，对模型的结构不需更改。经实验发现，该方法具有以下优点：

  1. give rise to improved generalization and faster convergence;
  2. to find better local minima of a non-convex training criterion.

#### comment:
  1. curriculum learning核心是如何判定样本的学习难易，文中从noise、样本的形式（图形旋转、扭曲）、词频等角度给出了实验，个人不得不惊叹该方法的简洁与可用性；
  2. 个人理解，在employ该方法时，可猜想要使“模型参数、结构简洁”该如何操作；
  3. 文中也对为什么该方法可行做出了猜想，个人看法是，容易学习到的sample是基础，构成了整个收敛面的basin，而tough sample相当于是高层面的样本，先基于简单的样本去学习，尽量保证往后的学习中不会偏离这个基本的basin。

#### highligt:
  1. A theoretical motivation for deep architectures comes from complexity theory: some functions can be represented compactly with an architecture of depth k, but require an exponential size architecture when the depth is restricted to be less than k.
  2. Erhan et al. (2009) found that unsupervised pre-training makes it possible to start the supervised optimization in a region of parameter space corresponding to solutions that were not much better in terms of final training error but substantially better in terms of test error.
  3. From the machine learning point of view, once the success of some curriculum strategies has been established, the important questions are: why? and how?
