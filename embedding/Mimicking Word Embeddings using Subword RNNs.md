#### note:
&nbsp;&nbsp;&nbsp;&nbsp;针对词向量的OOV情况，作者提出使用已有词的向量训练“字符级”有监督的模型来预测位置词的向量（详见paper第3部分）：Formally: given a language L, a vocabulary V ⊆ L of size V , and a pre-trained embeddings table W ∈ R^(V×d) where each word wk is assigned a vector e^k of dimension d, our model is trained to find the function f : L → R^d such that the projected function f | V approximates the assignments f (wk) ≈ e^k . Given such a model, a new word wk∗ ∈ L\V can now be assigned an embedding ek∗ = f(wk∗). 模型结构如下：

![](https://github.com/xwzhong/papernote/blob/master/pic/mimick%20model%20architecture.png)

#### comment:
&nbsp;&nbsp;&nbsp;&nbsp;相比于[Bite Pair Encoding](https://github.com/xwzhong/papernote/blob/master/others/Neural%20Machine%20Translation%20of%20Rare%20Words%20with%20Subword.md)，文章提出的解决OOV的方案有点曲折，使用word2vec或fasttext等其它算法预训练词向量后还需要有监督地训练向量拟合模型


#### more:
&nbsp;&nbsp;&nbsp;&nbsp;[代码](https://github.com/yuvalpinter/Mimick)
