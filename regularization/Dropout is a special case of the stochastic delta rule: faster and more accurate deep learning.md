#### note:

&nbsp;&nbsp;&nbsp;&nbsp;文章指出dropout是随机delta规则(stochastic delta rule)的特例。

&nbsp;&nbsp;&nbsp;&nbsp;dropout数学分布上的解释：To put the Dropout algorithm in probablistic context, consider that a Bernoulli random variable over many trials results in a Binomial distribution with mean np and standard deviation (np(1 − p)). The random variable is the number of removals (“successes”) over learning on the x axis and the probability that the hidden unit will be removed with Binomial (np, np(1 − p)).

&nbsp;&nbsp;&nbsp;&nbsp;相比dropout，stochastic delta rule的分布参数不固定，SDR adaptively updates the random variable parameters for subsequent sampling and Dropout samples from a Binomial random variable with fixed parameters (mean, standard deviation at p)，在实现时大致步骤如下：
  + a. 初始化每个参数方差为0，（此后更新时，以当前loss反向计算的梯度进行更新）；
  + b. 对于当前参数，以其当前值（作为正态分布均值）和参数方差（作为正太分布方差）进行取样，取样后的值即为更新后的参数值。

#### comment：
  1. 本文是缓解“过拟合”难得的好文，从理论上看有依据，同时从实验的准确率看表现异常好；
  2. 从论文分析可知，其假定每个神经元服从同样的分布，个人认为这是收敛速度加快的主要原因，同分布减小了参数的搜索空间；
  3. SDR也有点类似于[adversarial training](https://github.com/xwzhong/papernote/blob/master/regularization/Explaining%20and%20Harnessing%20Adversarial%20Examples.md)，SDR是将梯度反馈到参数上，对参数进行一定范围的随机，而adversarial training则是将梯度反馈到输入的样本特征中，对样本本身引入额外因子；
  4. 使用SDR约需额外一倍的内存（显存），用于保存梯度不为None的trainable参数的方差；
  5. 文章虽然指出，达到相同准确率时SDR模型不需要过多的epoch，但是每个epoch的计算量应该比基本模型高一倍左右（需要进行额外一次的反向梯度计算）。

#### more:
  1. [经典防过拟合方法Dropout，只是SDR的特例](https://zhuanlan.zhihu.com/p/43083693)
  2. [tensorflow code](https://github.com/noahfl/densenet-sdr)

#### question:
&nbsp;&nbsp;&nbsp;&nbsp;该策略在文本上不对word embedding使用SDR会不会好点？原因在于SDR是针对神经元上的操作。但是从dropout实际使用来说，对word embedding进行dropout也能达到缓解过拟合的情况；

#### highlight:
&nbsp;&nbsp;&nbsp;&nbsp;The proposed sequence generation model generates labels sequentially and predicts the next label conditioned on its previously predicted labels. Therefore, it is likely that we would get a succession of wrong label predictions in the following time steps if the prediction is wrong at time-step t, which is also called exposure bias.
