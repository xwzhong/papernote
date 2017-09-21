### Layer Normalization

#### note:
&emsp;&emsp;针对DL模型training时间长的问题，作者提出使用layer normalization的方式提高训练速度。该方法与batch normalization有个极大的不同：与batch size大小无关，从而有以下有点：
  1. training过程中，可使用较小的batch size，不用考虑sample之间的依赖;
  2. test过程使用layer normalization的过程与training完全相同。
  
&emsp;&emsp;具体操作：针对每一个sample，以layer为单位（假设有m个hidden unit），计算当前step该layer下m个unit pre-activity的均值和方差，m个unit共享得到的均值和方差并进行标准化。

#### comment：
  1. 该方法很好地摒弃了mini-batch大小的限制；
  2. 在RNN单元何处使用layer normalization时，paper的做法类似[Recurrent Batch Normalization](https://arxiv.org/abs/1603.09025)，而且得到的实验结果不错；
  3. paper fig6进一步证明batch size越大，模型性能越好；
  4. 经实验发现，LSTM使用layer normalization后，在其它参数相同的情况下，效率降低1.x以上。[更多讨论](https://www.reddit.com/r/MachineLearning/comments/4ufmxy/layer_normalization_implemented_in_tensorflow/)

#### highlight:
  1. Notice that changes in the output of one layer will tend to cause highly correlated changes in the summed inputs to the next layer, especially with ReLU units whose outputs can change by a lot.
  2. under layer normalization, all the hidden units in a layer share the same normalization terms µ and σ, but different training cases have different normalization terms. Unlike batch normalization, layer normaliztion does not impose any constraint on the size of a mini-batch and it can be used in the pure online regime with batch size 1.
  
