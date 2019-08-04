#### note:
　　文章介绍了由word vector生成sentence vector的方式，并着重介绍了max pooling和hierarchical pooling：
  1. max pooling。对句子中的词向量相同维度取max；
  2. hierarchical pooling。借鉴ngram方式，在指定大小的窗口中取average pooling，最后在所有ngram单元中取max pooling。
  
#### comment:
  1. 其提出的hierarchical pooling方式能顾及部分语序信息，但针对长度≤窗口k的句子则学不到语序信息。
  2. max pooling策略在dl中经常用到，没却没有过多的解释，文章4.1.1详细分析了max pooling学到的权重特点：
  + a. 学习到的权重更稀疏（大部分为0）；
  + b. 同一纬度权重最大的前5个词表明了其一般属于相同类别。
  3. 词序对sentiment classification相比于主题模型更重要。

#### highlight:
  1. Simple pooling operations are surprisingly effective at representing longer documents (with hundreds of words), while recurrent/convolutional compositional functions are most effective when constructing representations for short sentences.
  2. Sentiment analysis tasks are more sensitive to word-order features than topic categorization tasks. However, a simple hierarchical pooling layer proposed here achieves comparable results to LSTM/CNN on sentiment analysis tasks.
  3. To match natural language sentences, e.g., textual entailment, answer sentence selection, etc., simple pooling operations already exhibit similar or even superior results, compared to CNN and LSTM.
  4. In SWEM with max-pooling operation, each individual dimension of the word embeddings contains interpretable semantic patterns, and groups together words with a common theme or topic.
