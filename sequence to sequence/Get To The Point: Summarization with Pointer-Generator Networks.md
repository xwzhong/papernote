#### note:
　　作者提出使用Pointer-Generator Networks生成文本摘要，动机是摘要部分的词多为OOV词，使用pointer networks在seq2seq decoder部分既能得到预先定义的vocabulary中各词概率分布，也能使用copy机制，直接从encoder中复制某个词：
  1. encoder：对input进行encode，得到各个step的输出(e1, ..., en)；
  2. decoder：对当前step，vocab的概率分两部分（式9）：
      a. 常规方法计算得到的vocab各词概率；
      b. 使用(e1, ..., en)计算当前decoder步下各ek的权重，每个权重对应encoder位置的概率。
  3. loss：为了避免生成的内容出现了连续重复的句子，loss添加了额外的损失，名为converge loss。

#### comment:
  1. 该方法在decoder部分，既能生成指定vocab中词，也能主动在encoder部分直接copy，如果decoder中的词大部分来自encoder，而且oov词较多，使用该方面能较好的解决上述问题（适用范围）；
  2. 该方法巧妙的地方是vocab词与encoder中的词结合部分，其直接在原始的vocab中加权后进行拼接。

#### [code](https://github.com/abisee/pointer-generator)

#### highlight:
　　In this work we propose a novel architecture that augments the standard sequence-to-sequence attentional model in two orthogonal ways. First, we use a hybrid pointer-generator network that can copy words from the source text via pointing, which aids accurate reproduction of information, while retaining the ability to produce novel words through the generator. Second, we use coverage to keep track of what has been summarized, which discourages repetition.

