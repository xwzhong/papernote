#### 1. 先根据要求(准确率,速率)定模型整体方向

&emsp;&emsp;有些项目中,就算是能提高0.5%也是很大的改进,那么这种模型偏重准确率,而在有些任务中,准确率可以稍稍低一点(可能有其它方面弥补这块的损失,或这分类任务仅仅只是庞大系统的一小块),但因要兼顾整个系统的效率,实时性要求较高.当然,最好的选择是准确率最高同时实时性也最好.

#### 2. 准确率 vs predict时的速率

&emsp;&emsp;使用复杂深度学习重点考虑的是其分类准确率(数据表述更细致,参数更多), fasttext更多注重时间效率(c实现,w2v理论,OOV解决较好,使用n-gram考虑了句子中的词序,能解决部分数据不平衡问题,多分类中可以使用层级结构提高效率等, 相比SVM等经典机器学习算法在描述文本能力上更细致);

#### 3. 模型优化

&emsp;&emsp;怎么判定一个新模型/优化方案是否能提高准确率?

  + a. 考虑优化的思路是否切合数据的特点.比如,情感分类中使用VSM模型,如果再引入词序特征,准确率有很大的可能性提升,原因很简单,"喜欢不"和"不喜欢"表达的是不同的情感,而VSM模型描绘不出语序信息; 
  + b. 接下来还要考虑,这种语序信息对整个分类任务影响的比例有多大,如果仅占万分之一,那么优化的意义不大,因为每引入一个假设,必然增加模型一定的error,关键是得确定优化的部分要尽可能大于这个error; 
  + c. 最后还要考虑优化时,所用的表达方式能否正确代表优化的点,假设一句话的语序信息使用一个标量来表示,而原始的VSM维度上千维,那这个标量在整个分类模型中的作用非常有限(在此并不是说使用一个标量就能正确描述一句话的语序信息,仅做参考)

#### 4. 数据预处理
##### 文本
&emsp;&emsp;以是否影响分类结果为标准判定预处理技巧的选取,从而达到减轻模型训练负担(参数个数,训练时间),按理来讲,数据越复杂,不规律,比如线性不可分相比与线性可分,则模型所需参数,训练时间(特别是深度学习模型)更多.

  + a. 假设文本中有繁体,简体,而分类判断对字体不关心,只关心其所述内容,那可将繁体转化为简体,同理大小写,全角字符转半角字符都是常用的技巧;
  + b. 对于更深层次的,假设文本中有url,那是否需要剔除这些url也是根据上述标准,假设url对文本判定无影响,那可直接剔除,假设有影响,而且可以根据域名就能判定该url倾向于哪个类别,为了减轻模型训练负担,可直接提取域名,因为url多余的字符可以理解为噪音;
  + c. 某一类字符串,虽然形式不同,但是其含有相同的含义也可进行统一映射,此处是根据最终任务的目标反推判断;
  + d. 仅用指定字符集,eg:仅用中文;
  + f. 连续字符压缩后有无影响?eg:啊啊啊啊啊啊啊->啊啊啊(用正则一行代码搞定, 连续相同的多字符串同理)
  + g. 按字还是按词切分?以词为单位, 其包含的语义信息更完整,但量多(中文词以十万记,而常见字仅有3k左右), 以字切分有一个优点,对于模糊数据也能很好处理(eg: '伟.哥'分词后得不到'伟哥'这个词), 在深度学习分类模型中可优先考虑按字切分,同时加大模型结构(因为word embedding的表述空间小了,则需要模型更强的学习能力). 提到这个,在seq2seq中,如果decode部分的vocabulary非常大,则模型训练时间,内存/显存将要求更大, 当然也有sampling的方式缓解这个问题,但个人观点毕竟是取样,存在一定的信息损失.
  + h. 文本切分后保留长度.在深度学习中,训练往往是以batch方式进行,在考虑保留长度时需考虑在该长度文本下,文本保留的信息(重点),机器内存/显存的限制和训练时间.文本长度可取95%左右文本都能涵盖的长度,原因:在保证足够的信息被保留的情况下,减少长尾数据对训练时间的制约;注意,如果文本是由多个子文本拼接而来,需要使用拼接后的文本计算;

##### 非文本
&emsp;&emsp;非文本此处指格式化的数据,如星期,日期,次数,时间长度等,此处分两类:

  + a. 标量表示. 如时间长度,其为跨度值,不能用枚举的方式表示.对于能用标量表示的特征,需要进行映射,往往使用z-score,使其均值为0,方差为1,也可以使用函数映射到指定范围,对于某些特别重要的特征,可扩大其映射范围;
  + b. 元数据表示.如星期几, 此类数据暂称元数据,它的特征是使用枚举的方式得到. 元数据首先不用标量来表示,因为枚举特征之间的模型距离无法衡量, 以前常用的是用one hot(一个星期有七天,可用七个维度表示,对应的星期几赋值为1,其余为0), 但其表达元数据特征之间的关系仍是定量的,有一种比较好的方式是使用embedding,使用过程类似word embedding,只是将word换成了元数据. 在训练模型的过程可以不断学习元数据embedding的表示,达到自我学习的过程.有一点需要注意,某些非文本数值特征使用'标量表示'不一定合理,需从该特征的实际意义来理解并判断用何种表达方法;对于元数据特征embedding维度,可与其枚举数等同.

#### 6. 深度学习模型结构相关
  + a. 激活函数的选择和及其参数初始化. dl模型中相比于梯度爆炸,梯度消失问题更棘手.梯度爆炸可通过clip方式有效缓解,而对于梯度消失,其本身难以检测.2009年[Glorot](http://proceedings.mlr.press/v9/glorot10a/glorot10a.pdf)分析了激活函数与其参数初始化对模型的影响,其中通过实验表明tanh激活函数在使用指定的初始化方式的情况下能有效避开梯度消失,并加快模型的收敛速度([笔记](https://github.com/xwzhong/papernote/blob/master/neural%20network/Understanding%20the%20difficulty%20of%20training%20deep%20feedforward%20neural%20networks.md)),keras有相关该论文初始化方法实现(tf已含有keras模块).(注意,激活函数的选择,初始化策略还与输入数据每个维度的取值范围有关,这点paper好像没有提及,但个人感觉也是比较重要的一点,一般会将各个维度"0均值标准化",即将各个特征转化为"均值为0,方差为1",这个策略不是必要操作,可根据实际的任务仅对某部分特征进行标准化).关于各不同激活函数可视化及优缺点分析可见[链接](https://www.jiqizhixin.com/articles/2017-10-10-3).
  + b. RNN变体的选择-simple RNN, GRU和LSTM. simple RNN有天然的缺陷,可以不用考虑.有相关[实验](https://arxiv.org/pdf/1412.3555)([笔记](https://github.com/xwzhong/papernote/blob/master/neural%20network/Empirical%20Evaluation%20of%20Gated%20Recurrent%20Neural%20Networks%20on%20Sequence%20Modeling.md))表明,GRU在某些任务上效果比LSTM更好, 到具体任务时可实验测试,但论文中比较常见的是使用LSTM单元, 如果机器显存,计算能力足够,建议使用LSTM;
  + c. 单向RNN还是双向RNN结构. 单向LSTM仅考虑了已出现的文本,而双向结构则考虑了后续待生成的问题(虽然带生成文本未显示得出),运用中常用双向结构;
  + d. word embeddings.
      + ① 如何初始化分类模型中的词向量-使用word2vec等模型训练还是随机初始化比较好?拿word2vec来说,其训练得到的词向量否定词之间的空间距离比较接近,对于否定词敏感的任务来讲,此时最终分类模型训练得到的结果会打一定折扣,此时可以考虑随机初始化词向量,对比两者差异. 关于训练word2vec训练情感分析的词向量,可参考论文-Learning word vectors for sentiment analysis, A. Sentiment classification based on supervised latent n-gram analysis, Re-embedding words.
      + ② 词向量训练方法的选择;训练词向量建议使用fasttext,其相比于word2vec主要的优点是缓解OOV,因其使用subword表示,使得到的结果兼顾了词的形态信息,这点在错字中有出奇的效果,当然前提是这个错字词能被正确分词,同理,如果token仅仅只是label,在形态上没有间接的语义关联,那么效果会变差.2017年12月出了一篇[论文](https://github.com/xwzhong/papernote/blob/master/embedding/Advances%20in%20Pre-Training%20Distributed%20Word%20Representations.md),介绍了word2vec在考虑Position-dependent Weighting, Phrase representations及Subword information情况下的效果,实验结果令人欣喜;
      + ③ 更新词向量与不更新-一般选择更新参数;有论文介绍说结合更新和不更新两种方式能得到更优的上层结果, 更新向量参数能使得到的词向量往上层结构偏移,使之更好拟合上层问题,不随模型更新可更好利用原本训练好词向量语义信息(能学到什么程度与所用词向量模型有关,eg:word2vec, glove和fasttext),个人认为,最好能在上层模型训练到一定程度的时候随上层模型更新词向量参数,原因:上层模型在初始化相关参数后,除词向量含有一定先验知识,其它参数是混沌状态,刚开始训练时,词向量需要兼顾这些混沌状态得到的模型最终结果,而这初始阶段的最终结果一般不是最优的,可想而知词向量在开始训练阶段将被污染,在上层模型不断训练过程中,词向量再往最进一步的优化,如果是刚开始不对词向量进行调整,等上层模型训练到一定程度的时候再进行调整或许能缓解这种影响,目前还没做相关实验验证;
      + ④ 使用什么语料训练word embeddings?可以使用分类数据本身训练,有可以使用大型,规整的语料(eg:新闻,百科).已有人实验得出,使用分类数据本身也能达到大语料训练得来的效果.使用大型公开语料,首先数据量多,其次这些类数据比较规范,模型学到的语义信息也更规范.(ps:[400w搜狐新闻](http://blog.sina.com.cn/s/blog_16d74e01f0102x1js.html))
      + ⑤ 对于OOV词,在分类模型中该如何初始化?对于fasttext不存在这个问题的考虑,因为其使用n-gram方式解决OOV词,哪怕这个OOV词拆分后的gram没有出现在fasttext模型中,每次它也能唯一返回一个词向量.对于word2vec, 本人试过使用随机初始化,最大最小值为已在word2vec模型的词向量中的最大最小值. 但看到论文"Convolutional Neural Networks for Sentence Classification"提到这样一句话:When randomly initializing words not in word2vec, we obtained slight improvements by sampling each dimension from U[−a, a] where a was chosen such that the randomly initialized vectors have the same variance as the pre-trained ones.(如果谁有自己的见解希望[在这里分享下](https://www.zhihu.com/question/68711290)), 在yoonkim提供的代码中,a取值为[0.25](https://github.com/yoonkim/CNN_sentence/blob/master/process_data.py#L95).
  + e. 使用什么优化方案sgd还是adam? sgd收敛速度慢, 容易陷入局部最优, 困于鞍点, 针对这些问题的改进方案有Momentum(动量),NAG,Adagrad, Adadelta, RMSprop, Adam, AdaMax, Nadam等等, 初步调参可使用adam, 其理论,解决的方面相对较多,同时强烈建议细读论文[An overview of gradient descent optimization algorithms](https://arxiv.org/abs/1609.04747)([笔记](https://github.com/xwzhong/papernote/blob/master/neural%20network/An%20overview%20of%20gradient%20descent%20optimization%20algorithms.md)).
  + f. 模型调参.
      + ① epoch或训练步数的选择.训练模型前,将数据集分三份-训练集,验证集和测试集(可使用划分比例7:1:2).测试集用于评估在当前参数条件下,模型训练到最好时的效果.而这个"最好"的位置(具体是哪个epoch或step)是由"验证集"来确定的.在训练过程中,可在每个epoch结束或在指定间隔step后计算验证集的准确率,综合考察整个训练过程,选择验证集准确率最高的那个epoch或step模型结束训练位置.在训练实际上线模型时,由于使用了百分百数据集,其对应的epoch或step也可增加一点.
      + ② 词汇表大小.词汇表获取严格来说不能用验证集和测试集;一般的文本数据集其词汇由词频统计可发现长尾现象,选取词汇时,先由词频由大到小排序,取前k个词,使前k个词的词频和占总词频的指定百分比以上即可(可取98%). 从另一个角度解释,该策略能在尽量保存多信息的前提下剔除更多的tough信息.对于被剔除的词,可用UNKNOWN等字符串代替或直接跳过,对于文本较长的数据,比较建议直接跳过,文本较长本身还有信息量比较多,剔除UNKNOWN token可减少训练时间.
      + ③ batch size设置. 在神经网络算法原始的推导是使用整个batch计算梯度,限于运行内存/显存、单步更新速率，从而使用了mini-batch，个人实验发现，mini-batch越大，收敛速度越快，原因是更大的mini-batch更能代表模型整体收敛方向. 如果内存/显存允许，可尽量调高mini-batch数。但也不要忘记对同一个epoch进行shuffle操作，降低同个mini-batch样本与样本间的相互影响；同时,对于64, 128, 256, 512...等数值也是比较建议使用,主要考虑了内存的结构设计,能稍微提高训练速度(embedding size, rnn cell size等同理).
      + ④ learning rate. 论文"Don't Decay the Learning Rate, Increase the Batch Size"提到,batch size随训练步数的增加,可以使用较大lr,相当于lr可以维持不变.但是一般的训练任务应该用不上这个技巧,因为其说的batch size在实验中是以千或万来记. lr的选取一般不需要太大,常见的初始化值有0.001, 0.01, 0.1, 1.0;
      + ⑤ learning rate decay. 一般取0.9, 0.99, 0.999, 0.9998, 在有些任务中, 0.99和0.999的实验结果可能差很远. tf提供了tf.train.exponential_decay字段调节lr.此处的lr decay需要结合lr的选取来定,如果lr本身很小,那么lr decay也需要相应减小, 特别是当lr非常小时,需特别注意lr decay的调节.
  + g. 是否对softmax层进行取样?判断是否使用该trick需要理解为什么会有"在softmax取样"这一说法.当时学者提出该trick是考虑到若softmax层对应的词汇表非常大, 则将训练过程中如果使用GPU则显存要求高,同时计算量特别大,每个word都需要计算一次,如使用语言模型和[seq2seq的decoder层](https://arxiv.org/abs/1412.2007)([笔记](https://github.com/xwzhong/papernote/blob/master/translation/On%20Using%20Very%20Large%20Target%20Vocabulary%20for%20Neural%20Machine%20Translation.md)).因此,在softmax层output size比较小(以千记)可不使用取样,因为既然是取样自然会有损失在其中.
  + h. 是否使用batch normalization或layer normalization.有论文提及batch normalization[用于RNN hidden2hidden层效果不好](https://arxiv.org/abs/1510.01378)([笔记](https://github.com/xwzhong/papernote/blob/master/regularization/Batch%20Normalized%20Recurrent%20Neural%20Networks.md)),也有[论文](https://arxiv.org/abs/1603.09025v5)([笔记](https://github.com/xwzhong/papernote/blob/master/regularization/Recurrent%20Batch%20Normalization.md))指出其用于input2hidden对模型准确率,时间效率都有提升, 其中之一BN作者提出了BN的改进版[Batch Renormalization](https://arxiv.org/abs/1702.03275)([笔记](https://github.com/xwzhong/papernote/blob/master/regularization/Batch%20Renormalization:%20Towards%20Reducing%20Minibatch%20Dependence%20in%20Batch-Normalized%20Models.md)),建议在选择的时候使用Batch Renormalization或[layer normalization](https://arxiv.org/abs/1607.06450)([笔记](https://github.com/xwzhong/papernote/blob/master/regularization/Layer%20Normalization.md)).layer normalization在tf中已有实现,但个人在使用时发现,其需要非常高的内存,同时,单个batch计算效率明显下降,可在最终优化好的模型中测试是否使用normalization技巧.

#### 7. 加速模型训练的一些技巧
  + a. 对于文本数据,先用程序将词或字转化为id,训练模型时直接读入这些id,在训练过程中再进行转化非常耗时,特别是对于每个epoch都要进行id转化的代码.
  + b. 如果训练数据比较少,可直接读入内存中,并在训练前进行id转化;反之可通过转化为id后存入文本,或使用tfrecord, tfrecord对数据进行特定形式编码,存入文件中,读取时可按batch,多进程读取.
  + c. 课程学习. 其思想是:在训练过程中,先使用简单的部分数据训练,到一定程度后再用整个训练数据集.这个思想非常好,建议阅读论文[curriculum learning](https://ronan.collobert.com/pub/matos/2009_curriculum_icml.pdf)([笔记](https://github.com/xwzhong/papernote/blob/master/regularization/curriculum%20learning.md)),该思想不仅实践简单,而且对我们日常标注语料,清理数据有很大的指导作用, 如:相同文本出现在正负类别中该如何处理.课程学习要想实际运用需要思考:如何定义一个问题的难易程度,可从数据角度和分类器角度考虑.从数据角度可思考词频,从分类器角度,以分类器判别难以为准.这里可以提一下[IRGAN](https://arxiv.org/abs/1705.10513)([笔记](https://github.com/xwzhong/papernote/blob/master/chatbot/IRGAN%EF%BC%9AA%20Minimax%20Game%20for%20Unifying%20Generative%20and%20Discriminative%20Information%20Retrieval%20Models.md)),在思想上有共通之处.
