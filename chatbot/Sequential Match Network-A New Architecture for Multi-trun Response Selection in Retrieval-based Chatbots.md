### Sequential Match Network-A New Architecture for Multi-trun Response Selection in Retrieval-based Chatbots

#### note:
&emsp;&emsp;paper的摘要提到，基于检索的方式多轮会话中，所得到的回复忽略了与之前会话内容之间的“关系”以及各自的“重要性”。“关系”体现在，给出正确的回复时，之前的会话彼此之间的关系；而重要性则提现在，正确的回复与之前对话之间的关系。作者提出的解决思路如下：

1. “重要性”-a.以词来衡量；回复和每一个utterance的词转化为embedding后，计算两两词之间的相似度，得到矩阵A。b.以句来衡量。回复（utterance亦同）使用GRU encode，每个step的hidden state与每个utterance所有hidden state计算一个相似度。得到矩阵B。
2. 对1中得到的2-D矩阵（A、B）使用CNN降维，得到n个m维的向量（n为之前的会话轮数）
3. “关系”。使用GRU（n个m维的input）来描述赋予“重要性”后的会话关系。

#### comment:
1. paper提出的architecture使用了n*(GRU+CNN)+GRU的结构（n为之前的会话轮数），从表达能力讲，尽可能地把观察到的结构已表示出来，自然带来的一个负面影响是复杂度的提高，由于本人没实验，引用作者原话：Compared to generation models, discriminative models are much faster due to its small hidden states. Although our model is complicated, it can converage in 8 hours on a K80 GPU. Our model spends 200ms to predict 200 instances (1 batch) in the test process. In general, performance is not an issue if you have a GPU.
2. 在描述“关系”中，作者使用了三种不同的方法进行比较，这种比较方式可取。
3. 文章第4部分还给出了response candidate的检索方式，值得借鉴。

#### more reading:
<http://wennei.com/w6/2017-05-17/374016.html>

#### [code](https://github.com/MarkWuNLP/MultiTurnResponseSelection)
