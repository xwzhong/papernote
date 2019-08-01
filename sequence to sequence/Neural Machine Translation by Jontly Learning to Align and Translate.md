### Neural Machine Translation by Jointly Learning to Align and Translate 

#### note:
&emsp;&emsp;basic seq2seq把input信息都encode进“一个”固定的vector中，其vector本身的表达能力有限，特别是针对input句子本身比较长的情况，句子越长，vector信息越模糊。paper提出的解决方案是在decoder的每一个step中，不仅考虑decoder在该step之前得到的connection信息s和输入y，还对encoder部分“每一个”STEP进行回顾，并判定各个STEP隐层信息的权重、加权求和，得到该decoder部分step下的输入。

#### comment:
1. jointly怎么理解？需根据attention引入的方式来解释（attention就是加权求和后的c），在我看来就是这个加权求和过程；
2. 猜想。如果encoder-decoder中，两边的词是一对一的对应（或接近一对一），那么模型的效果会比“一对多”和“多对一”好一点。对于一词多义的情况，需要利用好上下文信息，而rnn正有这样的优点；
3. 该模型对长句子效果好，短句子是否可考虑不用该模型？得清楚长短在此文的界限。根据论文的fig2可知，对于句子长度为10的文本，该模型已经有很大的提升，长度为10已经挺短的，因此一般都会使用attention机制；
4. appendix中对如何employ c进行了详细的公式解说，非常值得看；
5. 本文是难得一遇的好文，对basic seq2seq有明显的提升效果。
