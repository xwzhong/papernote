### A Simple But Tough to Beat Baseline for Sentence Embeddings

#### note:
&emsp;&emsp;paper提出了一个很简单的sentence embedding方法（见原文Algorithm 1）：

  1. 使用无监督学习的方法计算word embedding，eg：word2vec，GloVe；
  2. 对待表示的句子，将每个词的词向量加权求和，每个词的权重仅用到了词的概率和人为设定的参数a；
  3. 对第2步得到的句向量使用PCA或SVD进行微调。

#### summary：

1. 在一般任务中，对句子的word embedding使用tfidf方式进行加权比求平均更优；
2. paper提出的方法中，不同训练集得到的word embedding适用于与其不同domain的数据；
3. paper提出的方法因为沿用了word2vec或GloVe，因此自然也保留了其无监督方法的特点，如反义词的word embedding相似，造成在情感分析的任务中表现较差；
4. 论文4.3部分以词序作为变量在多组不同任务（similarity、entailment、sentiment）中进行了实验，可知词序对这些任务都有助提高；
5. 通过table5、6对比可知
  + a. tfidf-GloVe有20个（总数为26）比GloVe-W更优，因此猜想tfidf+GloVe+R会有最优结果；
  + b. Twitter数据在GloVe+R中比所有模型高20%左右，这点值得思考；
     
6. SNLI数据集[leaderboard](https://nlp.stanford.edu/projects/snli/)显示，sentence embedding方法最高为84.6%（2017-07-20），本方法为78.2%；
7. paper所提出的方法确实比较简单，但也给出了相应的理论证明，在某些任务上表现不错。总之，需就待解决的实际问题来选择使用哪方面的方法，考虑是否使用word embedding，词序，tfidf，PCA/SVD等等，需分析什么时候需要，什么时候不需要。

#### highlight:
  1. Use word embeddings computed using one of the popular methods on unlabeled corpus like Wikipedia, represent the sentence by a weighted average of the word vectors, and then modify them a bit using PCA/SVD.
  2. To estimate cs, we estimate the direction c0 by computing the first principal component of c˜s’s for a set of sentences.
  3. We also note that the top singular vectors c0 of the datasets seem to roughly correspond to the syntactic information or common words. For example, closest words (by cosine similarity) to c0 in the SICK dataset are “just”, “when”, “even”, “one”, “up”, “little”, “way”, “there”, “while”, and “but.”
  4. Finally, we speculate that our method doesn’t outperform RNN’s and LSTM’s for sentiment tasks because (a) the word vectors —and more generally the distributional hypothesis of meaning —has known limitations for capturing sentiment due to the “antonym problem”, (b) also in our weighted average scheme, words like “not” that may be important for sentiment analysis are downweighted a lot. To address (a), there is existing work on learning better word embeddings for sentiment analysis (e.g., (Maas et al., 2011)). To address (b), it is possible to design weighting scheme (or learn weights) for this specific task.

#### question:
&emsp;&emsp;pca/svd担当的角色主要是什么？
  
#### code
  1. [theano](https://github.com/PrincetonML/SIF)
  2. [sklearn](https://github.com/peter3125/sentence2vec)
  3. 使用tf实现可用到tf.svd
