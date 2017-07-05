### A Knowledeg-Grounded Neural Conversation Model

#### note:
&emsp;&emsp;paper提出使用data-driven和knowledge-grounded方式（23M general dialogue dataset+1M grounded dialogue dataset+1.1M tips），使seq2seq生成更加contentful的response，大致思路如下：
  
  1. 对post信息进行encode，得到vector u；
  2. 使用post文本信息检索与之相关的tips（根据tf-idf计算相似度得到），并用式2得到vector c；
  3. 使用u计算各个c的权重，并进行加权求和（式4），最终相加得到seq2seq中decoder部分的隐层输入（式5）。

#### comment:
  1. paper提出了使用post“相关的其它信息”使生成的回复更具实质内容，这个出发点不错，引入其它信息从某个角度讲是降低了post的“熵”；
  2. 模型在deploy某个post的其它information时，用了类似attention的机制，每条tip信息输出权重由post得到的vector u衡量，这一trick在多篇paper都有体现，而且效果还不错；
  3. 用BLEU作为对话系统的衡量指标，paper最好的BLEU得到为1.08，而翻译模型其BLEU一般在30+，使用BLEU评价生成式对话系统的好坏确实有失偏颇。
