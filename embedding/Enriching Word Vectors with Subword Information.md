### Enriching Word Vectors with Subword Information

#### note:
&emsp;&emsp;paper提出了一种改进基于word2vec的方式。核心思想是使用了subword信息。简单来讲，假设有两个词“火影忍者”和“忍者”，由于这两个词存在交集，使用subword方式便将这两者内在的语义联系起来，而不需要这两个词都出现的语料。实现比较简单，仅需在原有代码的基础上，使用n-gram的方式修改数据的输入，eg：“火影忍者”的2-gram表示——<火,火影,影忍,忍者,者>，其中<和>分别为起始和结尾标识符。

#### comment：
  1. subword的优点：
      * a. 学习到词与词形态学方面的信息，词与词交集越多，且语义相近的数据集，其效果越好。（可查看sisg-的效果）
      * b. 较好解决OOV的情况，对于长尾数据是很好的补充。（可查看sisg的效果）
  2. 论文在四个任务上进行了比较——word similarity, word analogy, morphological reresentation, language model, 有以下结论：
      * a. 不考虑OOV的情况（sisg-），模型提高约3+%左右，考虑OOV（sisg）模型提高约4+%。
      * b. 在word analogy任务中，syntactic方面的准确率提高更明显，最多能提高22%+。
  3. n-gram是用在词内部，不是用在词与词之间，所以能学到的是词内部中部分顺序信息。扩展到词与词用n-gram方式便可得到带顺序的句向量(不知道实际的效果在特定任务上效果如何?经思考,如果扩展到词用n-gram,内存要求比较高,对于2-gram,假设中文词有10w,则有10的十次方个token)。
  4. 文中虽然对n的选择进行了分析，但n的选择用于中文仍需实验得到，标准——对最终任务的提升效果。
  5. 该策略为fasttext的一部分，gensim上已有代码实现，可直接调用。
  6. 既然使用subword学习到的是形态学信息，如果其信息是完全不相关的，是不是该把这部分数据剔除，例如人的姓名。

#### highlight:
  1. A vector representation is associated to each character n-gram; words being represented as the sum of these representations.
  2. Most of these techniques represent each word of the vocabulary by a distinct vector, without parameter sharing.
  3. In particular, they ignore the internal structure of words, which is an important limitation for morphologically rich languages.
  4. As expected, the nearest neighbors for complex, technical and infrequent words using our approach are better than the ones obtained using the baseline model.
  5. we observe that the most important n-grams correspond to valid morphemes.
