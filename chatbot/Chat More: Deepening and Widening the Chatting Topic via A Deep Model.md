#### note:
&emsp;&emsp;paper针对生成式闲聊问题，主体架构以seq2seq模型为基础，提出了一种使回复更deep和wide的方法。fig1详细地介绍了deep和wide的含义，所谓deep就是使之前会话的内容进行更深层次的分析（如果此前提到了下雨，这时可强调“雨确实是大”，wide即从此前话题进行关联扩展（针对上文提到下雨，可回复“你带伞了吗？”）。该模型主要分四部分：
  1. 使用tf-idf进行关键词提取（此前的历史会话暂称为history，当前回合用户说的话为post，待回复为response）。history+post中提取到的关键词构成context keyword集合，由context keyword集合筛选得到deeper keyword，最后由response提取得到wider keyword集合；
  2. global channel。用GRU对句子信息进行编码，得到所有词的高维输出；
  3. deep channel。从context keyword到deeper keyword过程，用了MLP组件计算context keyword各个词的权重；
  4. wide channel。用attention based RNN结合global channel信息+context keyword来预测wider keyword。
  
#### comment:
  1. paper提出的方法过于依赖关键词，在实验部分，也是根据关键词进行了筛选（在response中至少包含大于某阈值的两个keyword）;
  2. post加入resp keyword训练，进行rerank时通用性回复score仍然较低，比较合理的方式可能是限制性条件下定向选取。

#### more:
  1. [通过深度模型加深和拓宽聊天话题，让你与机器多聊两句](https://www.jiqizhixin.com/articles/2018-04-24-4)
  2. [Chat More: Deepening and Widening the Chatting Topic via A Deep Model (code)](https://sigirdawnet.wixsite.com/dawnet)
