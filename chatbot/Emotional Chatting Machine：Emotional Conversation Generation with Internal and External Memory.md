### Emotional Chatting Machine：Emotional Conversation Generation with Internal and External Memory 

#### note:
&emsp;&emsp;paper把resp的emotion信息embed到一个高维的向量，提出了三种不同的方法来deploy这向量：
1. emotion category embedding。计算resp的情绪类别，并将该类别转为指定维度向量v跟decoder部分的word embedding放在同一级嵌入到seq2seq中；
2. internal memory。将1得到的情绪向量v在生成时逐步递减，最后降为0；
3. external memory。将decoder部分的词典分为不相交的通用和情绪词典，根据预先计算的情绪显示控制每个step输出的word。

#### comment:
1. paper的亮点是可以根据预先设定的情绪来生成文本，由被动化为主动；
2. 个人意见，所提到的三种方案中，emotion category embedding从可扩展性，合理性讲都比较好；方案2中，使用向量来表征情绪本身就是抽象的，一个向量全为0不一定等于“没有情绪”；
3. 所提方案确实能降低perplexity，因为引入了response中的信息；
4. 论文有些表述不敢苟同，可能写得还不够细致，流程图解释得也不够，如fig3中M是怎么引入到式16的。

#### more reading:
<https://610300.kuaizhan.com/5/82/p426375651610fb>

#### [code](https://github.com/loadder/ECM-tf)
