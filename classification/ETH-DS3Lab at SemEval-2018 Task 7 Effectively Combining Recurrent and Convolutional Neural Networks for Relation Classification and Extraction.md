#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper是semeval-2018竞赛文章，在关系抽取比赛中取得不错的成绩。文章出彩的地方不是提出了什么新颖的结构，而是整合多方面的模块放大其效果。
  + 1. 整体结构：word->信息抽取（词、词性、与实体词的位置关系）->embedding编码->rnn和cnn分别输出各个类别的概率->整合rnn和cnn概率得到最终输出。详见下图：
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Effectively%20Combining%20Recurrent%20and%20Convolutional%20Neural%20Networks%20for%20Relation%20Classification%20and%20Extraction.png)
+ 2. 各个模块整合策略：
    + ensemble。使用不同的初始化参数，训练k个分类器，最后对各个类取平均值作为对应类的概率。（文中尝试了1<=k<=30的情况，经测试最好的效果时k=20时）
    + word embedding。作者下载了同领域数据，测试发现，word2vec 200维的结果相比于100维和300维F1值更高。（300维的效果相比于200维差了+2%F1）
    + 预处理：
      + 裁剪句子。作者通过分析Subtask1.1发现，拥有实体关系的词随着彼此距离的增加样本数越来越少，为了减少非实体关系判为实体关系的情况，仅考虑小于一定长度阈值的句子
      + 实体标签。在实体词前后插入特殊的标签，用来明确指明中间的词为实体词
      + 相对位置策略和类别数。
      + 词性。将每个明确的词性用特定向量表示，类似于word embedding
    + 充分利用已标注数据。由于“SemEval-2018 Task 7”中关系分类的数据较少，作者整合了Subtasks 1.1和1.2的数据（+3.6%F1）
    + 生成额外数据。将实体对直接与另一句子的实体对替换（+0.7%F1）
    + 参数优化。使用网格搜索方式进行调参
    + 修改loss设计。因各个类含有的数据非常不均，而使用的交叉熵与最终的衡量标准F1有一定的差异，同时考虑到F1对数据量少的类别比较敏感，因此在训练时加大数据量少的类别影响（+1.6%F1）
    + upsampling。仍旧是为了缓解数据不均问题（+12.2%F1）

#### comment:
  1. rnn和cnn的整合策略并不是最后一个向量concat，而是输出的概率根据句子长度加权——since the RNN-based architecture had a tendency to obtain better results than its CNN-based counterpart for long sequences, we combined both predictions in such a way that a higher weight was assigned to the RNN predictions for longer sentences.
  2. 为解决关系分类问题，大部分策略在不同任务中是通用的（eg：实体识别，chatbot，其它类型的分类等），但作者尽量将各项技巧都发挥到最好的效果（多实验验证），需要考虑在后期工作中秉持这种科学的态度和并将公共模块抽取出来；

#### question:
  1. A shortcoming of this approach is that the cross-entropy loss usually only constitutes a conveniently decomposable proxy for what the ultimate goal of the optimization is (Eban et al., 2017): in this case, the macro-averaged F1 score. 怎么理解这句话？

#### more:
  1. [文章概述](https://zhuanlan.zhihu.com/p/35845948)
