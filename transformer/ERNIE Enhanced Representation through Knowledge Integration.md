#### note:
&nbsp;&nbsp;&nbsp;&nbsp;针对BERT模型，ERNIE提出两点改进：
  + 1. 中文层面，BERT进行mask是基于字的。对于实体词中某个字进行mask的样本，模型很容易根据实体词中其他字预测被mask的部分，比如：阿里[MASK]巴，很容易推测[MASK]为“巴”，因此ERNIE提出对实体词进行mask。
  + 2. 增加训练语料来源：百科、新闻、论坛对话类数据。

#### comment:
  + 1. 文章提出的idea比较简单，但是效果提升明显，针对中文数据，使用分词策略也能达到实体词mask的效果；
  + 2. 目前百度已经ERNIE模型通过蒸馏的方式用于搜索场景中，据说效果还不错。

#### more:
  + 1. [ERNIE预览：百度 知识增强语义表示模型ERNIE](https://www.jianshu.com/p/fb66f444bb8c)
  + 2. [提速1000倍，百度飞桨发布基于ERNIE的语义理解开发套件](http://baijiahao.baidu.com/s?id=1649525069184443515)
