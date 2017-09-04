### Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift

#### note:
&emsp;&emsp;作者主要想通过减小deep network中layer与layer之间的covariate shift来加快模型训练的速度。提出的原因是：layer的输入分布本身的变化导致其参数也需要相应的调整，注意此处说的变化，是指“分布”的变化，比如线性分布转为双曲线的分布。paper提出的解决方案是在每个unit进行计算激活值前（称为pre-activation)，先对其进行normalization操作，使其均值为0，方差为1，有点像zero-score，考虑到在整个training set进行normalization可行性不高（内存，运算时间，更新时效等），所以在batch层面进行，所以叫做batch normalization。

#### comment：
  1. 文章讲了该方法提出的很多理论，对深入了解神经网络很有帮助，同时非常建议研读“Understanding the difficulty of training deep feedforward neural networks”；
  2. paper提出的方法有以下特点：可使用更大的learning rate值（更高的lr也对应了更快的decay），加速模型训练（能加速并不特指增加了lr本身，还有其它因素），正则化（从而能降低其它正则化的强度，如dropout，l2等）；batch size不能太低（个位数），理论上越高越好。
