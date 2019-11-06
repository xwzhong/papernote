#### note:
&nbsp;&nbsp;&nbsp;&nbsp;针对串行训练的multi-task，考虑到不同任务优化的方向不同，当前task B可能会使已达到最优超参平面的task A远离，因此提出elastic weight consolidation（EWC）改进策略：
  + 1. 前提：任务A和任务B存在较优的公共解区间
  + 2. 方案：在当前step k（任务A已经训练完），任务B的梯度反向传播时，对于任务A重要的weight施加较小的影响（参数更新幅度小）
  + 3. 操作：
    + a. 对于任务A，按照常规方法训练，达到解空间x
    + b. 对于任务B，先确定解空间x对任务A的重要程度F（利用任务A的验证集，计算x的梯度，然后取平方，换言之，梯度越小，该参数更接近任务A的最优解，因此越重要），并记录解空间x的具体数值star，然后在计算任务B的loss时新增对旧任务的consolidation。
    + c. 针对任务C、D...，重复step b

#### comment:
  + 1. 文章提出的观念比较新颖，其中的理论推导相比[代码](https://github.com/ariseff/overcoming-catastrophic)难理解一点，针对多任务，但有不共用的参数部分需要留意。

#### more:
  + 1. [tf示例代码](https://github.com/ariseff/overcoming-catastrophic)
