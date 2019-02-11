### Using the Output Embedding to Improve Language Models

#### note:
&emsp;&emsp;paper提出了一种改进RNN语言模型的方法,该方法操作简单,只需'连接'模型input embedding和output embedding.其给出该方法的核心思想是:

&emsp;&emsp;_We call U the input embedding, and V the output embedding. In both matrices, we expect rows that correspond to similar words to be similar: for the input embedding, we would like the network to react similarly to synonyms, while in the output embedding, we would like the scores of words that are interchangeable to be similar (Mnih and Teh, 2012)._

#### comment:
  1. 其思考角度翻译过来就是,对于output embedding, 如果词与词之间相似,那么在softmax层对应的score也应该相近,直接将word embedding与output embedding进行tying,相当于显示地利用了已训练好的word embedding相似关系,同时减少了参数. 使用显示tying input和output embedding也能看出模型学习能力的不足;
  2. 论文第三部分提到使用projection regularization能对模型进行微调(在lstm output后添加全连接层),但不仅限于此, 论文提到使用tying技巧需要rnn的output hidden size和embedding大小相同, 但在实际运用中, hidden size往往比embedding size大,此时可以通过添加全连接层进行调整,使输入最后softmax层的维度等于vocaburary size;
  3. 文章提出的思想不仅可以用于rnn结构的语言模型,也能用于类似rnn结构的其它模型中,在LSTM+CRF实体识别模型中,使用该技巧能提高0.01左右的F1 score;
  4. "Following (Zaremba et al., 2014), we employ two models: large and small. The large model employs dropout for regularization. The small model is not regularized." 个人对此持有异议:large相比于 small model有更强的表达能力,softmax能较容易地描述其特征,而small模型内部结构复杂,此时使用projection层相当于搭建lstm输出和softmax之间的桥梁.

#### more reading:
&emsp;&emsp;[Tying Word Vectors and Word Classifiers: A Loss Framework for Language Modeling](https://github.com/xwzhong/papernote/blob/master/neural%20network/Tying%20Word%20Vectors%20and%20Word%20Classifiers:%20A%20Loss%20Framework%20for%20Language%20Modeling.md)

#### [code](https://github.com/ofirpress/UsingTheOutputEmbedding)
