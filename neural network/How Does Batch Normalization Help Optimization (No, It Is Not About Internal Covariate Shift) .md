#### [highlight](https://mp.weixin.qq.com/s/7obF_oxk5BrF3R-kbAsRrw):
　　作者研究了BatchNorm能提高深度神经网络训练有效性的根源，并发现BatchNorm与internal covariate shift之间的关系是微不足道的。特别是，从优化的角度来看，BatchNorm并不会减少internal covariate shift。相反，BatchNorm对训练过程的关键作用在于其重新规划了优化问题，使其Lipschitzness（BatchNorm对损失函数稳定性的影响）稳定和β-smoothness更有效（“有效”在这里指，朝梯度方向移动时测量梯度的变化），这意味着训练中使用的梯度更具有良好的预测性和性能，从而可以更快速、有效地进行优化。

　　同时，作者也展示了这种平滑效果并不是BatchNorm特有的，其他一些自然正则化策略也具有相似的效果，并能带来可比较的性能增益。
