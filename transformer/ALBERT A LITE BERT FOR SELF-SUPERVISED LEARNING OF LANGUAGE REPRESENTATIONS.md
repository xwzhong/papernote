#### note:
&nbsp;&nbsp;&nbsp;&nbsp;针对bert显存占用高、训练慢，作者提出了两个改进策略，同时针对句子之间的连贯性问题提出了对next sentence task的改进策略：
  + 1. Factorized embedding parameterization（对word embedding进行因式分解）：word embedding用较小的dim参数E，然后映射到transformer隐藏层大小H，参数量从O(V\*H)变为O(V\*E+E\*H)，当H远大于E时，参数降低非常明显（在实验中，作者始终将E设为128，即使是albert-base）；
  + 2. Cross-layer parameter sharing（transformer层与层之间共享参数）；
  + 3. Inter-sentence coherence loss（句间连贯性损失）：bert中next sentence task更多学到的是主题分类任务，因为负样本是从其他文章中随机选取的，从而对“句子之间的连贯性”信息学习不足（因为已经可以通过主题将两个句子分开）。因此作者提出sentence-order prediction（SOP）任务，该策略正样本构造跟原bert方法一样，负样本为正样本句子顺序调换。


#### comment：
  1. 作者提出的第一个策略“Factorized embedding parameterization”，解释感觉有点牵强，给人的印象是：为了降低显存，降低了word embedding大小，然后实验效果还行；
  2. 文章给出的时间，是指总的训练时间减少（因为训练步数减少，共享层与层之间的参数有点像batch normalization策略），而不是同数据量预测时间减少；

#### more:
  1. [作者提供的源码](https://github.com/google-research/ALBERT)
  2. [中文预训练ALBERT](https://github.com/brightmart/albert_zh)
