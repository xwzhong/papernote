### Learning to Generate Reviews and Discovering Sentiment
#### note:
  
1. 文章使用Amazon商品评论数据(38G)训练了一个1层4096个unit的语言模型，这4096个unit中，发现了一个sentiment unit，能指示待encoded中每个字（或词）的情感极性（正面或负面），另外该句子encoded后，还能判断整个句子的情感极性，在IMDB数据集上，错误率降低到7.7%（state of art 方法为5.91%）；
2. 训练好语言模型后，通过很少的标注数据（30个）就能超过在Stanford sentiment treebank数据集下的state of art方法；
3. 在使用语言模型生成句子时，能通过人工直接控制sentiment unit的值来决定所生成文本的情感。

#### comment:

1. 语言模型仍有很多未知的潜力，对于hidden unit，我们对其仍知之甚少；
2. 文本中没提及如何寻找这个sentiment unit，但是可以尝试使用已标注的相近领域情感分类数据来找；
3. 其它unit是不是也反映了数据在某方面的特点，已知的有句子长度，会包含语义上的转折unit？
4. seq2seq会不会有同样的unit？
5. 如果language model有很多理想的unit（大家想通过这些unit来控制生成），是不是会有lang2seq模型（language to sequence）,这样既利用了language model能用大量数据无监督学习的特点，还能利用seq2seq end2end的特性。

#### practice：

1. 通过领域训练得到的language model在特定领域使用时，如果语料的overlap不高，效果不一定特别好，因此可在通用领域训练好的model基础上，用待解决问题领域的数据进行fine tuning。其它运用还有word2vec。
2. 利用好这个已发现的sentiment unit，不仅可以减少人工标注数据来训练情感分类器，还能直接控制文本生成等等。

#### more reading:
<http://it.sohu.com/20170407/n486996650.shtml>

#### [code](https://github.com/openai/generating-reviews-discovering-sentiment)
