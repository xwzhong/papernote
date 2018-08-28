#### note:
　　本文是一篇survey文章，介绍了任务型和非任务型使用深度学习的主流技术路线，其中非任务型主要包含以下几点：
  1. seq2seq（用pair对训练，但会出现生成多样性-一直觉得这个是伪命题、上下文一致性，同时在其中可引入主题，情感，dialog act等信息，除了生成，也可改成rank形式，这方面Google有多篇paper）
  2. memory network（也是用pair训练，但通过memory机制引入了额外信息，除了生成，也可改成rank形式，这方面Facebook有多篇paper）
  3. retrieval-based（在特定的知识领域运用较多，而且相对成熟，如：客服领域）

#### comment:
  1. 文章所在概述算是比较全面，比较建议非任务型方面再加一篇2017年3月份的论文：[Learning Discourse-level Diversity for Neural Dialog Models using CVAE](https://github.com/xwzhong/papernote/blob/master/chatbot/Learning%20Discourse-level%20Diversity%20for%20Neural%20Dialog%20Models%20using%20Conditional%20Variational%20Autoencoders.md)，个人认为CVAE是一个不错的方向；
  2. 非任务型生成式有因“信息不足”有各种缺陷，检索式在大语料下会给人出乎意料的惊喜，但不够细致，结合此两者就目前来讲或许是不错的商用方案。
