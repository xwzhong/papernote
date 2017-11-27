### Convolutional Neural Networks for Sentence Classification

#### note:
&emsp;&emsp;paper在fig1架构的基础上,通过实验分析词向量在CNN文本分类中对准确率的影响,词向量所做的实验设置如下:

  1. CNN-rand: 词向量随机初始化并在训练分类器中不断更新；
  2. CNN-static: 词向量使用100B词训练好的word2vec初始化,并保持不变,对于未在pre-train出现的词,随机初始化;
  3. CNN-non-static: 初始化方式与2相同,但在分类器训练过程中不断更新;
  4. CNN-multichannel: 每个词使用两个词向量表示(使用pretrain word2vec),其中一个词向量随分类器不断更新,另一个则保持不变.

#### comment:
  1. 相对于pretrain词向量, 随机初始化的方式始终是最差的(其中还包括SST情感分析任务,虽然在SST1中提升不多-至少0.5%).
  2. 使用非当前任务的语料(此处为100B Google news)训练word2vec,能得到该语料的一些特征,将该word2vec用于其他任务的问题中,如果使用的是static方式,训练得到的分类模型更多是利用了其它语料的embedding信息,而non-static方式,则兼顾了其它语料及当前语料的信息,但是训练方式的缘故,仍会造成学习上的偏差,体现在:如果该pretrain的词向量是最好的,但因分类器本身并不直接在该embedding下得到最优结果,导致pretrain的词向量出现偏移.因此作者也提出,怎么样尽可能地利用pretrain信息以及该task本身的信息.
  3. paper提出的"CNN-multichannel"方式正是想解决comment2提出的问题,实验中确实也取得一定的效果;
  4. 文章要是能使用各个任务的语料,专门训练其对应的word2vec进行实验比较,或许能发现更多信息,印象中有实验表明,使用其对应的语料训练word2vec效果也不错;
  5. 在实际使用中,我们拥有大语料(eg: 几百万的新闻,上千万的百科数据),而实际待解决的任务可能是特定领域的, 此时是不是也可以在大语料训练好的word2vec基础上,再使用具体任务的语料进行增量训练,通过适当的调整,也能解决pretrain的词向量出现大量OOV的情况(大语料和具体任务的语料同时训练,最后再使用具体任务的语料微调).
  6. table3对CNN-multichannel训练完分类器的结果进行分析,有一个有趣的发现:bad原本与good在空间分布中很接近,但在训练分类器中经过non-static后,bad最终与terrible很接近,是不是可以使用这种方式来解决word2vec训练得到的词向量其反义词相近的情况?non-static在各个任务中表现都不差.
  7. pretrain的word2vec语料可尽可能选择与待解决问题在语法,语义上相近,有助于提升最终的准确率.

#### hightlight:
  1. Dropout consistently added 2%–4% relative performance.
  2. we obtained slight improve- ments by sampling each dimension from U [−a, a] where a was chosen such that the randomly initialized vectors have the same variance as the pre-trained ones.([detail](https://github.com/yoonkim/CNN_sentence/blob/master/process_data.py#L88), why???)
  3. Adadelta (Zeiler, 2012) gave similar results to Adagrad (Duchi et al., 2011) but required fewer epochs.([更多介绍](https://github.com/xwzhong/papernote/blob/master/neural%20network/An%20overview%20of%20gradient%20descent%20optimization%20algorithms.md))

#### [code](https://github.com/yoonkim/CNN_sentence)

#### more reading:
[卷积神经网络用于文本分类](http://blog.csdn.net/cyl9413/article/details/53432640)
