#### note:
　　文章还是针对seq2seq结构在闲聊领域中的问题。闲聊中，说出当前句子背后有很多额外的知识，但是seq2seq不能对这部分信息进行有效编码（个人观念是某些信息在当前pair中既不会出现，也很难从pair推理得来），针对这个问题，作者提出使用隐变量z来代替这个未知的信息（CVAE），同时在此基础上，为了方便训练（出于正常情况训练语料少），提出显示表征隐变量z的策略（kgCVAE）：
  1. CVAE：
    a. 训练——对resp进行编码，经recognition网络得到分布z，使用KL拟合prior网络分布z'（用于测试），结合z和encoder输出对resp进行生成;
    b. 测试——使用prior网络随机输出分布z'，结合z'和encoder输出进行生成；
  2. kgCVAE：
    a. 训练——在CVAE基础上，主动引入resp的细粒度信息（此处为dialog act），由细粒度信息推算其分布y，用y影响z生成，同时y、z和encoder输出对resp进行decode，利用MLPy主动拟合分布y
    b. 测试——由MLPy生成细粒度信息（dialog act）分布y'，再由y'、z'和encoder输出对resp进行decode。

#### comment:
  1. 作者的思路非常好，知道单纯的pair缺失了很多信息，因此考虑使用隐变量来表示这种差异（如果是一对一，或近似一对一问题，eg：翻译，那么这种差异就没那么紧迫）；
  2. 根据实验结果，CVAE虽然能明显降低perplexity（相对于simple seq2seq），但在BLEU等评测中结果与baseline相近，这也是正常的，虽然CVAE中隐变量能编码这些信息，但是测试集中post-resp对是固定的，隐变量随机后的分布不一定刚好是resp对应的分布；
  3. kgCVAE是一个好的方向，在隐变量z和resp中间再加入了其它信息的分布，其实这个分布y是显示地告诉模型去生成符合分布y的结果，更高层面讲是生成符合指定dialog act的句子，可能作者甚至想直接根据输入的某些类型（eg：情感，句式等）直接生成句子，照这样发展，需要剖析一个句子的生成跟什么因素相关。

#### more:
  1. [《Learning Discourse-level Diversity for Neural Dialog Models Using Conditional VAE》阅读笔记](https://zhuanlan.zhihu.com/p/26898768)
  2. [code](https://github.com/snakeztc/NeuralDialog-CVAE)
