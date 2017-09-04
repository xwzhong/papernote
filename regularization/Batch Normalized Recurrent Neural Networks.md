### Batch Normalized Recurrent Neural Networks

#### note:
&emsp;&emsp;作者探讨了在RNN中使用batch normalization的可行性，经实验，作者指出对“simple rnn”的hidden2hidden层的每个activation function进行batch normalization时，其训练速度不减反曾，准确率也略微变差，因此作者提出只在input2hidden层进行标准化（详见式18，同时针对multi layer rnn，只对纵向的变换使用normalization操作，类似dropout）。实验结果表明，测试准确率基本没有提升。

#### comment：
  1. paper对hidden2hidden引入batch normalization进行了实验，其结果却出乎意料地差，其中的缘由值得思考，原文给出的解释是“It may be due to the fact that we estimate new statistics at each time step, or because of the repeated application of γ and β during the recurrent procedure, which could lead to exploding or vanishing gradients.”。从个人从看的paper出发，觉得原因是pre-activation的计算直接糅合了hidden和input的信息，而这两个方向的信息不应该“直接相加计算normalization”，因为它们两个的分布是不一样的，可以考虑单独进行normalization后再进行相加（recurrent batch normalization这篇论文会有实验）。
  2. paper提出的sequence-wise normalization策略不错，可用在其它填充序列进行batch计算的方法。
