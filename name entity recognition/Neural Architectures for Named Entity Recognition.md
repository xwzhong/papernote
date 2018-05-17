#### note:
&emsp;&emsp;这是一篇使用深度学习进行实体识别的经典论文, biLSTM+CRF结构. 原理比较简单, 先使用biLSTM结构得到每个char/word的logit输出, 输出的维度对应tag个数, 然后使用CRF计算最优路径.

#### summary:
##### 1. 简评
&emsp;&emsp;biLSTM+CRF进行实体识别思路比较简单, 在简单优化的情况下就能超越之前精雕细琢的模型.

##### 2. "为什么少量的数据(以千计)便能得到良好的实体识别效果"

  + a. 前提: 如果仅根据当前句子本身可利用的信息便能识别出实体, 那么使用识别算法的效果便可做一定的预期, 这是一个很重要的前提, 可预期模型识别在现有标注语料下的识别上限, 正如翻译, 大部分情况下, 仅根据当前语料对训练便能得到较好的效果, 而在对话系统中, 同样使用seq2seq其效果却与翻译的结果相差很多;
  + b. 句子结构: 实体识别任务非常需要利用句子本身结构的信息, 整体数据的语法结构越规范, 模型学习后预测的效果会更好, 例如: '你在阿里巴巴工作吗?', 如果类似'在xxx工作'经常出现, 那么模型也会学到'在xxx工作'结构中, 'xxx'很可能代表公司;
  + c. 词语记忆: 所谓的记忆是指模型在训练语料中见过某个实体词, 若在预测新数据的时出现该实体词, 则能正确识别的可能性将非常大;
  + d. embedding泛化: 此处的泛化是由数据特点决定的, 如, 大部分人名的姓氏出自百家姓, 而这些字(词)可通过embedding预先学习到其相似特征; 时间也是同理, 时间内常包含数字信息, 而数字在embedding中相似的空间的结构能减轻模型学习的负担. 因此embedding在biLSTM+CRF中的重要性不言而喻;
  + e. biLSTM+CRF结构; 还有一个不能忽略的是biLSTM+CRF本身的结构, biLSTM能学习语序信息, 其双向结构能记忆上下文, 同时CRF也是非常优秀的统计算法, 在分词任务中已有实验证明其效果非常显著.

##### 3. 预训练

  + a. embedding

    + ① 该模型的准确率对embedding比较敏感, 使用与实体识别相似的大规模数据(G级别)训练得到的embedding, 比小规模, 不同类型(大规模)的数据更好;
    + ② 在训练biLSTM+CRF模型时, 建议不随模型更新embedding参数(embedding用大规模同类型语料训练得到), 其主要原因是固定同类型大规模语料训练得到char/word之间的关系, 经实验, embedding若一直是trainable将导致准确率下降; 也有学者提到在训练到一定epoch后再更新embedding参数, 个人发现针对同类型大规模得到的embedding, 该策略对F1值影响不大;
    + ③ 从embedding对模型的重要程度可知, 适当增加embedding的维度也是提高F1值不错的选择;
    + ④ 连接input embedding和output embedding也能提高模型的准确率, 可见[论文笔记](https://github.com/xwzhong/papernote/blob/master/neural%20network/Using%20the%20Output%20Embedding%20to%20Improve%20Language%20Models.md), 该策略的进阶版解释详见[链接](https://github.com/xwzhong/papernote/blob/master/neural%20network/Tying%20Word%20Vectors%20and%20Word%20Classifiers:%20A%20Loss%20Framework%20for%20Language%20Modeling.md);

  + b. 语言模型. 使用语言模型先对biLSTM结构进行预训练发现, biLSTM+CRF模型的拟合速度加快, 但是最终的F1值却有所下降, 关于这点个人仍十分怀疑实验的科学性, 待验证;
  + c. 词级别.

##### 4. batch size
&emsp;&emsp;该模型偏向于使用较小的batch size, batch size大虽然能加快模型的收敛, 但最终F1值却下降, 可见同个batch的样本彼此之间应该有较大的影响, 可考虑使用较小的batch size或使用normalization策略降低同个batch样本之间的互相影响.(更多解释见"[当前关注点：批量大小、学习率、泛化性能下降](https://www.jiqizhixin.com/articles/051303)"部分)

##### 5. projection layer
&emsp;&emsp;在biLSTM output到softmax之间添加前馈神经网络;

  + a. 原因; 结合论文[Breaking the Softmax Bottleneck: A High-Rank RNN Language Model](https://arxiv.org/abs/1711.03953)理解, biLSTM的输出为高秩, 直接连接softmax层对限制softmax的学习能力, 用个可能不恰当的比喻, 如, 线性可分模型训练非线性数据集将得到较差的结果;
  + b. 搭建"连接input embedding和output embedding"的桥梁; 原tying技巧直接将LSTM输出与word embedding连接, 这需要LSTM隐层状态维度与embedding维度相同(如果是biLSTM, 则embedding维度需为LSTM隐层状态维度的两倍), 如果希望LSTM隐层维度与embedding维度不相同, 可再加一层或多层前馈神经层, 此时不影响tying技巧的使用, 因为该技巧核心是input embedding与projection layer output相同.
  + c. 重新初始化projection layer参数, 对第K次训练好的biLSTM参数进行再训练; 此时biLSTM参数相当于已经站在比较好的收敛位置, 此时再初始化projection layer参数进行训练, 将使模型biLSTM+projection参数训练更好的拟合位置.

##### 6. tagging schemes
&emsp;&emsp;paper提到了两种打标签方式, IOB(inside, outside, begin)和IOBES(inside, outside, begin, end, singleton), 从5.a提到的论文出发, 个人也是推荐使用IOBES形式的打标签策略.

##### 7. 训练数据:

  + a. 标注标准; 不管是人工标注语料, 还是想合并从网上搜集得来的数据集, 其标注标准最好能一致, 比如, 对于别称"小李子", 数据集A不判定为人名, 而数据集B判为人名, 那么数据集A和B合并时, 总数据集内部便有两套标准, 从模型本身的角度出发, 训练数据存在歧义, 自然影响模型最终的预测.(如果数据集本身有很多模糊不定的样本, 要想让模型学习到'正确'的结果会不太现实, 而且训练数据一般比较少). 个人提倡一种"分得开, 合得拢"的标注思想: 以最小单元为标注思想, 往上层构建, 如:2018年4月8日, 可标注为: (2018年, 时间), (4月, 时间), (8日, 时间), 因为某些句子可能只提到了'2018年', 那么'2018年'便是共有的'子单元', 但是(2018年, 时间), (4月, 时间), (8日, 时间)又能完整地合并成一个时间, 就像原子通过组合成为分子. 另外说一个纠正数据的策略, 统计每个词属各个实体类型的分布以及同个类别下不同词的分布情况, 看看是不是有明显标注出错的部分;
  + b. 增加训练数据量; 除了网上提供的标准论文数据集, 针对具体业务, 一般需要手工来标注, 不言而喻, 增加训练集的数目能明显提高模型准确率, 针对中文短文本, 以千计的数据量便能得到0.915+的F1值. 如果针对一个具体领域的实体识别任务, 完全没有标注数据(一个原因是数据类型完全不同, 另一个可能是标注标准不同), 可使用网上已有的实体标注模型, 大规模标注, 筛选句子中实体较多的句子进行人工纠正, 这样做能有效地学习一个句子尽可能多的实体. 当有一定量的训练数据, 为提高模型准确率想继续标注, 此时要用训练的模型来预测新的数据, 对新数据中预测错误的样本进行纠正并学习, 该做法便能有针对性地优化模型没学习到的部分;
  + c. 不同实体类别的比例及子标签(eg: B-PERSON, I-PERSON等)的分布; 对于一般的对话文本, 其实体类别的分布应该是'时间', '地点', '人物'这三种类型占比较多, 而'公司名', '机构名'相对较少, 模型针对特定类别的识别准确率与其本身的数据量大小应该也有关系的(实际情况待验证, 这个点算是个人一些思考), 因此, 如果想让'人物'识别准确率高一点, 可以有针对性地提高该类别的数据量大小.

##### 8. char(字符)和word(词语)的结合
&emsp;&emsp;在汉语中, 可按char或word来构建biLSTM+CRF模型. 按char, 除了可减少embedding规模大小, 最主要的是能利用摆脱'分词'算法本身, 按word则可利用'词语'级别的语义信息, 但是如果一个词是一个tag, 如果分词本身不准确, 将明显影响实体识别的准确率. 在原论文中, 作者提出将'char'和'word'结合起来, 预测的时候对'word'打tag, 而在中文中要利用类似的结构则需要分词.

##### 9. 实体识别与分词算法的结合
&emsp;&emsp;可通过实体识别的结果来进行辅助性分词, 当实体识别训练数据达到一定程度后, 则可直接考虑"分词"+"实体识别"同时进行, 当训练数据较少的时候, 不推荐将分词直接引入到biLSTM+CRF中, 个人观点是基于大规模语料的统计分词会比小规模(以千记)类似实体识别语料效果应该要好, 虽然个人还没进行实验.


#### more reading:
  1. [NLP论文笔记1：Neural Architectures for Named Entity Recognition](https://blog.csdn.net/juanjuan1314/article/details/78905239)

