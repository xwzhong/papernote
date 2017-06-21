### Sequence to Sequence Learning with Neural Networks 

#### note:
&emsp;&emsp;本文是seq2seq比较原始版本，先使用一个rnn将一段文本映射到固定维度的vector中，再由另一个rnn将该vector作为初始状态进行decoder。同时，本文指出对encoder部分的input进行reverse能有更好的效果。

#### comment:
1. 本文得到的测试结果虽比现在（2017-06-21）state of art差得比较远（BLUE34.8vs41.29），但可从其所遇到的问题，了解attention、sample softmax等优秀的策略的提出背景；
2. paper提到使用reverse效果更好，从侧面指出rnn在长句方面仍有欠缺，而同期Bahdanau等人提出的attention机制刚好能在一定程度上弥补（bidirectional rnn也能弥补）该缺点；
3. model analysis部分，对于类似的句子，seq2seq encoder得到的hidden state在空间中聚合，这一点发人深省。

#### more reading:
<https://opensource.googleblog.com/2017/04/tf-seq2seq-sequence-to-sequence-framework-in-tensorflow.html>
