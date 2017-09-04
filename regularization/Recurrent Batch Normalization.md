### Recurrent Batch Normalization

#### note:
&emsp;&emsp;paper跟“Batch Normalized Recurrent Neural Networks”一样是探讨对RNN引入batch normalization后的效果，但其deploy策略表明，对模型准确率、训练速度都有较大的提升。从实现的方法上看，其对每个激活函数的input都进行了batch normalization（有sigmoid，tanh，详见式6-8）。

#### comment：
  1. 从式6可知，激活函数的均值为0，方差却为2，而不是1（两个方差为1但是不相关的分布相加其方差为2，均值为0），同时也侧面表明γ值需要相对较小，参数的初始化需要考虑的点比较多，核心是在当前loss function的基础上，w和x要相契合，w*x值太大，容易造成激活函数饱和，从而降低传播梯度，训练时间加大。
  2. 对比“Batch Normalized Recurrent Neural Networks”论文，其实验结果显示hidden2hidden中引入batch normalization效果差的原因还是这点：pre-activation的计算先对hidden和input的信息相加再进行batch normalization，而这两个方向的信息不应该“直接相加计算normalization”，因为它们两个的分布是不一样；
  3. 在inference中，population方式比batch statistics更好。

#### highlight:
&emsp;&emsp;Covariate shift is a change in the distribution of the inputs to a model. This occurs continuously during training of feed-forward neural networks, where changing the parameters of a layer affects the distribution of the inputs to all layers above it. As a result, the upper layers are continually adapting to the shifting input distribution and unable to learn effectively.
