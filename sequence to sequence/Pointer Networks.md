#### note:
　　Pointer Networks基于seq2seq with attention的结构，当前序列的输出集合为当前序列的输入集合，同时输出集合并没有像一般定义好的词集，而直接用位置索引替代，模型逻辑：
  1. encoder：对input进行encode，得到各个step的输出(e1, ..., en)；
  2. decoder：对当前step，使用(e1, ..., en)计算当前decoder步下各ek的权重，最大的权重位置对应的encoder输入即为当前decoder的输出（详见paper 2.3部分）。

#### comment:
  1. 该策略在凸包、旅行商问题中实验中效果良好；
  2. 其能很好的指向输入的unit，但限制在当前序列输入的unit，若其它序列中的unit未在当前序列出现，同样不能生成；
  3. 文章提出的策略非常巧妙，同时也说明seq2seq with attention策略虽然能考虑到某些方面，但针对特定问题，显示的表达想要的特征可能会得到意想不到的结果。
