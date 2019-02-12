
#### note:
&emsp;&emsp;文章一作者是word2vec的原作,在word2vec的基础上提出了一种准确,高效的模型.在CBOW模型中,预测的是中间词出现的概率,而fasttext中,则是预测对应文本的类别.同时fasttext使用了hierarchical softmax,每个叶子代表类别.

#### comment:
  1. fasttext效果好的原因探讨:

	  + a. fasttext虽然是线性模型,即使hidden unit很少,但其参数特别多,主要体现在每个词的embedding上,在训练的时候,词的embedding会跟着优化,这也是模型准确率高的一个重要原因,因为同个词在不同文本之间存在关联,而这种联系正是通过embedding建立;
	  + b. label之间的表示也彼此影响.因为在层次结构中,如果类1和类2存在公共路径,那么在训练类1文本的时候,必然更新公共路径部分的参数;
	  + c. [subword策略](https://github.com/xwzhong/papernote/blob/master/embedding/Enriching%20Word%20Vectors%20with%20Subword%20Information.md)。将词切分成subword形式，并且加入了尖括号<>在单词外面，因为这样可以区分前缀和后缀，比如一个单词where如果用3-gram来表示，那么可以表示为：<wh, whe, her, ere, re>;
	  + d. 文章使用了bigram策略,已有实验在[情感分类任务](https://github.com/xwzhong/papernote/blob/master/classification/Baselines%20and%20Bigrams:%20Simple%2C%20Good%20Sentiment%20and%20Topic%20Classification.md)中表明,该策略能部分描述语序信息,具体引入方式可见[N-gram特征，浅谈FastText文本分类利器解读（2）](https://blog.csdn.net/qq_43019117/article/details/82770124).

  2. 能较好解决类别多的分类问题(实验测试了312k个类别的分类问题);
  3. 文章没有实验使用预先训练好的word embeddings,如果用了,效果可能会有提升;
  4. 训练,测试速度相比CNN,RNN快几个量级.

#### highlight:
  1. we show that linear models with a rank constraint and a fast loss approximation can train on a billion words within ten minutes, while achieving performance on par with the state-of-the-art.(这里的rank constraint怎么理解??)
  2. However, linear classifiers do not share parameters among features and classes. This possibly limits their generalization in the context of large output space where some classes have very few examples(表明为什么类别多的问题能较好解决).
  3. On this task, adding bigram information improves the performance by 1-4%.

#### more reading:
  1. [NLP︱高级词向量表达（二）——FastText（简述、学习笔记）](http://blog.csdn.net/sinat_26917383/article/details/54850933)
  2. [fastText 源码分析](https://heleifz.github.io/14732610572844.html)
  3. [fastText库讲解](https://www.quora.com/How-does-fastText-output-a-vector-for-a-word-that-is-not-in-the-pre-trained-model)
  4. [all kinds of text classificaiton models and more with deep learning](https://github.com/brightmart/text_classification)
  
