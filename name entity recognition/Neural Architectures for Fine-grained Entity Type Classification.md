#### note:
　　作者提出了一种细粒度实体识别的方法，主要步骤如下：
  1. 对mention entity进行编码。原文是以英文为基础，以word为单位，将每个word使用embedding转为vector后，将所有vector对应维度相加并取平均。
  2. 对context进行编码。在原句子中以mention entity单词切分，分左右两部分词集left, right。使用bilstm分别对其进行编码（左右两边是不同的lstm参数），然后使用attentive机制对输出的hidden output进行加权，并归一化。
  3. 引入hand-craft特征（tab1）。
  4. 引入hierarchical label，使具有相似属性的实体label其参数能共享（原文fig2）。

#### comment:
  1. Fine-grained Entity Type Classification指细粒度的实体识别，比如常用的lstm+crf模型能识别人名，地名，而Fine-grained Entity Type Classification则进一步细分人名，如：医生，演员，作家等。
  2. paper提到，对mention entity进行encoding时选了相对粗糙的方法，是为了降低过拟合的可能。
  3. 步骤2中引入的attentive机制与seq2seq中引入的方式如出一辙，而且经本文实验发现，相比于averaging，attentive模型准确率提高8%+（tab3）。
  4. hand-craft特征对结果影响明显，根据数据不同，影响程度不同，甚至可能会降低acc（tab5）。

#### [code](https://github.com/shimaokasonse/NFGEC)
