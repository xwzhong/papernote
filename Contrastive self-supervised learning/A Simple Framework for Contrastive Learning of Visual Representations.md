#### note:
&nbsp;&nbsp;&nbsp;&nbsp;在图像领域，作者提出simCLR框架，在大规模无标注语料上进行自监督训练，结果表明微调模型后ImageNet数据集上表现优异，simCLR任务：
  + 1. 设计：将原图片进行增强，在同一图片扩展出来的子图中拉近它们的距离，在不同图片扩展出来的子图中推远其距离（如下图），相似度计算使用MLP后的cosine；
  + 2. loss：使用contrastive cross entropy loss（cosine除了一个temperature parameter）；
  + 3. 受益点：较大的批量、训练时长、网络深度、数据增加策略（迁移到文本中要多尝试）、在损失函数前采用基于MLP的非线性投影（但在finetune时丢弃该层表现会更好，详见原文fig2）

#### comment:
  + 1. 该论文较大的贡献在于少量标注数据集时，如何能尽可能地提高预测性能；
  + 2. 作者尝试了多种不同的变换策略，最终发现组合“裁剪”和“色彩失真”可以得到SOTA（单策略不会提高太多性能），说明如果要迁移到文本中，还需要进行多种尝试
  + 
#### more:
  + 1. [自监督学习](https://zhuanlan.zhihu.com/p/66063089)：直接从无标注数据中进行学习，eg：language model、next sentence prediction
  + 2. [论文解读](https://mp.weixin.qq.com/s?__biz=MzI3MTA0MTk1MA==&mid=2652065896&idx=1&sn=0b539317e18ea705744200dff8c0f8b9)
  + 3. [tf源码](https://github.com/google-research/simclr)

#### question:
  + 1. 为什么loss计算时sim要除以tau?
