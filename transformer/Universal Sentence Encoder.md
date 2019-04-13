#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper指出，使用[SNLI](https://nlp.stanford.edu/projects/snli/snli_1.0.zip)数据预训练[transformer](https://github.com/xwzhong/papernote/blob/master/transformer/Attention%20is%20All%20You%20Need.md)参数，对下游句向量编码的任务效果有明显的提升，要点记录：
  1. 使用SNLI数据预训练被证明有效：[Supervised Learning of Universal Sentence Representations from Natural Language Inference Data(2017-05)](https://github.com/xwzhong/papernote/blob/master/embedding/Supervised%20Learning%20of%20Universal%20Sentence%20Representations%20from%20Natural%20Language%20Inference%20Data.md), [Learning Semantic Textual Similarity from Conversations(2018-04)](https://github.com/xwzhong/papernote/blob/master/embedding/Learning%20Semantic%20Textual%20Similarity%20from%20Conversations.md)；
  2. 预训练sentence embedding比word embedding模型效果更好；
  3. 文中提出的预训练方法在下游任务中仅需少量标注语料便能获得较好结果，后续增加有标签的数据对最终准确率增长贡献小；
  4. 使用angular distance替代cosine衡量句子之间的相似度，更多解释可见[Cosine similarity vs angular distance](https://math.stackexchange.com/questions/2874940/cosine-similarity-vs-angular-distance)；
  5. [SST Bench](http://ixa2.si.ehu.es/stswiki/index.php/STSbenchmark)句子相似度数据集(dev0.814/test0.782), [BERT_base(test0.858), BERT_large(test0.865)](https://github.com/xwzhong/papernote/blob/master/transformer/BERT:%20Pre-training%20of%20Deep%20Bidirectional%20Transformers%20for%20Language%20Understanding.md)。


#### comment:
  1. 文章更像是一篇实验性文章，印证transformer+预训练SNLI的有效性；
  2. angular distance衡量相似度可考虑使用。

#### more:
&nbsp;&nbsp;&nbsp;&nbsp;[Cosine similarity vs angular distance](https://math.stackexchange.com/questions/2874940/cosine-similarity-vs-angular-distance): The problem with the cosine is that when the angle between two vectors is small, the cosine of the angle is very close to 1 and you lose precision...
