### LSTM-based Deep Learning Models For Non-factoid Answer Selection

#### note:
&emsp;&emsp;paper比较了在Q&A领域answer选取的几种方法，并提出了自己的model，总体思想是在计算Q&A cos相似度的情况下，使groundtruth与question的cos值，比unlabel的回复更大（见式7）,以下是计算cos的几种方式：
  
  1. QA-LSTM：分别计算Q&A biLSTM的hidden state，然后可按avg、max、head/tail三种方式获取向量（见fig1）；
  2. QA-LSTM/CNN：先用biLSTM获取hidden state构成一个矩阵，然后使用CNN获取合成后的向量（见fig2）；
  3. Attention-based QA-LSTM：对于question部分的vector q，用方法1获取，对于answer部分的vecter a，每个timestep的output都结合q进行计算，接下来可使用avg、max、head/tail三种方式合成；
  4. QA-LSTM/CNN with Attention：结合方法2和3得到。

#### comment:
  1. cosine similarity（式7）：最后的一层并不是通常的分类或者回归的方法，而是采用了计算两个向量（Q&A）夹角的方法。M是需要设定的参数margin，q、a+、a-分别是问题、正向答案、负向答案(准确地说是unlabel答案）对应的语义表示向量。损失函数的意义就是：让正向答案和问题之间的向量cosine值要大于负向答案和问题的向量cosine值，大多少，就是margin这个参数来定义的。cosine值越大，两个向量越相近，所以通俗的说这个Loss就是要让正向的答案和问题愈来愈"相似"，让负向的答案和问题越来越不"相似"；
  2. paper提出的方案比非DL state of art方案更好（insuranceQA和TREC-QA数据集）；
  3. 方法3引入了attention，扩展了attention这种机制的思维，非常不错；
  4. 试验中加入了不同文本长度做对比，非常有借鉴意义（结合insuranceQA test1和test2，方案3在answer文本长度小于55时表现更有优势）；
  5. 在QA-LSTM中，acc排序：max>avg>head/tail（相邻之间相差4%左右），head/tail在QA-LSTM attention中表现仍是最差，而max表现更优可能是因为max学到了更多局部、有用的特征；
  6. 4.3最后一部分指出使用了MLP计算，得到最终的分数，但效果不理想（作者提到可能是因为参数过多，难拟合）；
  7. Q&A共参数集。分析，同参最终得到的两个vec对应的维度表征都一样；
  8. 预训练语言模型效果会更好。

#### [code](https://github.com/sujitpal/dl-models-for-qa)
