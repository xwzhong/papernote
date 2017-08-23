### Supervised Learning of Universal Sentence Representations from Natural Language Inference Data

#### note:
&emsp;&emsp;paper提出使用SNLI（Stanford Natural Language Inference）数据训练inference模型，再用其中间产物来生成其它task的句子向量。该模型是在fig1结构下进行的。

#### comment：
  1. 从实验结果来看，通过该有监督学习方法得到的sentence embedding方式确实比无监督学习得到的sentence embedding在多个任务中效果更好，但是背后深层次的原理仍不能很明确地证明出来，一而概之可以说是SNLI为待构建的sentence提供了除该句子之外其它的信息（或者是能学到的，确定的模型同时也确定了其能表达、学到的内容），但是具体的理论证明仍需学者探索，同时也因为这个因素造成其不可控，难以运用在实际项目中；
  2. BiLSTM-max比mean、LSTM等表现更优。
  
#### highlight:
&emsp;&emsp;stacked RNN：The goal of a such model is to encourage each recurrent level to operate at a different timescale.

#### thought:
&emsp;&emsp;使用transfer learning时需要考虑以下几点，pretrain的information是否切合最终的问题，比如pretrain word2vec，如果只是通过简单的加权（mean或tfidf），反倒使情感分类的效果更差（因为word2vec弱化了情感正负面词之间的相似度），反之，pretrain的模型越切合待解决问题，最终的效果会越好，切合的角度有：数据来源（涉及到词分布、语法特点）、问题特点等。

#### highlight:
  * hypothesis：We hypothesize that the semantic nature of NLI makes it a good candidate for learning universal sentence embeddings in a supervised way.
  * reason：Models can be trained on SNLI in two different ways: (i) sentence encoding-based models that explicitly separate the encoding of the individual sentences and (ii) joint methods that allow to use encoding of both sentences (to use cross-features or attention from one sentence to the other).
  * BiLSTM-Mean does not make sharp choices on which part of the sentence is more important than others.

#### [code](https://github.com/facebookresearch/)
