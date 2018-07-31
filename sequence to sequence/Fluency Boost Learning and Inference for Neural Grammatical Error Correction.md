#### [main](https://www.jiqizhixin.com/articles/2018-07-22-10):
　　作者提出使用流畅度提升学习（fluency boost learning）来对句子进行纠错，其核心原理就是在训练模型的过程中，让seq2seq模型生成出多个结果，然后将结果中流畅度不如目标端正确句子的生成句子和目标端正确句子配对，组成全新的流畅提升句对，作为下一轮训练的训练数据。而流畅度提升推断（fluency boost inference）则是利用seq2seq模型对句子进行多轮修改，直到句子的流畅度不再提升为止。这种多轮修改的策略能够率先改掉句子的一部分语法错误，从而使句子的上下文更加清晰，有助于模型修改剩下的错误。

#### comment:
　　亮点主要有以下方面：
   a. 训练数据少的情况下，通过beam search生成多个结果进行再训练；
   b. 使用流畅度衡量当前句子与最终正确句子的差距，从而判断是否继续训练/生成（类似不断对句子进行纠正的过程）；

#### more:
  1. [通过全新学习和推断机制提升seq2seq 模型的语法改错性能](https://www.jiqizhixin.com/articles/2018-07-22-10)
  2. [机器语法纠错能力新突破，微软小英变身英语写作老师](https://www.msra.cn/zh-cn/news/features/engkoo-composition-score)
