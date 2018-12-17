#### note:
&nbsp;&nbsp;&nbsp;&nbsp;文章发表于2008年，提出将多项NLP任务（词性标注、分块、实体识别、语言模型[非常规语言模型]、语义相关词）一起训练来提高某项任务（语义角色标注[SRL]，因其较复杂）中的效果。大致过程：针对具体某项NLP任务，每个词有k个不同类型的特征，eg：词本身、首字母是否为大小写、与谓词的距离等，对每个特征进行embedding，然后使用神经网络进行训练。要点记录：
  1. 每项任务共用同一份“词本身”的embedding，从而达到jointly训练的效果；
  2. 语言模型不是利用前k-1个词来预测第k个词，而是判断句子中的词是不是与其前后文本相关。训练时，将句子A中间词用随机挑选的词替换后得到的句子B，优化方向是使A得到的score比B尽可能地＞1。


#### comment:
&nbsp;&nbsp;&nbsp;&nbsp;作者提出的语言模型新颖，该任务与SRL结合时比其它任务单独或一起训练都更好（详见原文tab2），该策略与[BERT](https://github.com/xwzhong/papernote/blob/master/transformer/BERT:%20Pre-training%20of%20Deep%20Bidirectional%20Transformers%20for%20Language%20Understanding.md)模型的masked language model有相近之处，或许借助神经网络强拟合能力，加上恰当的结构设计（目的是为了表示词、句子等信息）能得到出人意料的效果。


#### more:
&nbsp;&nbsp;&nbsp;&nbsp;Here, we only want to have a good representation of words: we take advantage of the complete context of a word (before and after) to predict its relevance.
