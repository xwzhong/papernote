#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper提出了一个对大模型（参数多）剪枝的策略（并不是降低参数的量，而是使参数值尽可能地为0，从而加快预测时的计算速度，也可以说是模型压缩）。该策略可从两个角度进行剪枝：
  1. Unit dropout：Unit dropout randomly drops units (sometimes referred to as neurons) at each training step to reduce dependence between units and prevent overfitting.
  2. Weight dropout（来源[dropconnect](https://github.com/xwzhong/papernote/blob/master/regularization/Regularization%20of%20Neural%20Networks%20using%20DropConnect.md)）：Weight dropout randomly drops individual weights in the weight matrices at each training step. Intuitively, this is dropping connections between layers, forcing the network to adapt to a different connectivity at each training step.

具体操作：
  1. 以magnitude来衡量unit/weight的重要性，unit pruning和weight pruning计算公式不同（分别为论文式1和式2）；
  2. train: 选取γ|θ|个最不重要的值，并以α概率进行dropout；
  3. eval: 直接将“γ|θ|个最不重要的值”设为0；

#### comment:
  1. train阶段，选出“γ|θ|个最不重要的值”时并没有将其全部设0是因某些元素在往后的训练中权重可能会上升。
  2. 实验表明，该方法相对于直接提高dropout进行剪枝有更好的鲁棒性——剪枝效果明显，但准确率下降幅度小。
  3. 就“dropout与Targeted Dropout关系”有个网友说得好：这个不是替换dropout的，dropout提出来的时候是为了防止overfitting的，这个是用来做模型压缩的，不是一个东西。

#### more:
  1. [Dropout可能要换了，Hinton等研究者提出神似剪枝的Targeted Dropout](https://zhuanlan.zhihu.com/p/50796723)
  2. [tensorflow code](https://github.com/for-ai/TD)。核心代码是[dropouts.py](https://github.com/for-ai/TD/blob/master/models/utils/dropouts.py)。
