### Batch Renormalization: Towards Reducing Minibatch Dependence in Batch-Normalized Models.md

#### note:
&emsp;&emsp;paper作者是原batch normalization方法提出者之一，其指出原有的BN在training过程中具有以下缺点：

* batch size设置需较大；
* 样本与样本之间存在依赖的问题。

&emsp;&emsp;造成上述两者的原因，作者猜想：that is due to the dependence of model layer inputs on all the examples in the minibatch, and different activations being produced between training and inference。提出的改进方法是在train和infer过程中employ BN步骤建立映射关系。详见论文第3部分。

#### comment：
  1. 在建立映射关系时，作者很巧妙地引入了infer过程中的μ和σ。
  2. 在training过程中，如果没有特别要求，尽量保持每个训练的batch彼此之间都不同，不仅是同一个epoch，不同epoch之间同理。
  
#### highlight:
  1. However, its effectiveness diminishes when the training minibatches are small, or do not consist of independent samples.
  2. Let us observe that if we have a minibatch and normalize a particular node x using either the minibatch statistics or their moving averages, then the results of these two normalizations are related by an affine transform.
