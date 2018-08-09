#### note:
　　文章提出了一种word向量更丰富的表示，主要步骤如下：
  1. 预训练：使用大型语料训练bi-lstm语言模型；使用时，固定bi-lstm参数，获取bi-lstm的输出，经映射并加权相加后得到x的上下文（contextualized）信息y（详见式1）；
  2. 针对特定任务，原本是将x输入rnn（与预训练使用的bi-lstm参数不共享），现在将x与y拼接后再输入，或与x经rnn计算后得到的输出h拼接，以此来利用x在当前句子中的上下文信息。

#### comment:
  1. 从实验的结果上看，该方法在阅读理解（Liu），语义角色标注（He），实体识别（Peters)，细粒度情感分类（5类，McCann)模型中提升明显；
  2. 从直观上分析，该方法是从细致化角度表达了word的上下文，该细致化主要归功于lstm的输出（高层次表达)，而且通过一定的实验证明了其有效性，但仍像是黑匣子，难以从理论上去分析其原因。

#### more:
  1. [论文主页](https://allennlp.org/elmo)
  2. [tensorflow code](https://github.com/allenai/bilm-tf)
  3. [tensorflow hub调用（需网络，没中文）](https://www.tensorflow.org/hub/modules/google/elmo/2)
