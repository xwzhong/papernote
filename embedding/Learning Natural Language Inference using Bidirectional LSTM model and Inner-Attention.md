### Learning Natural Language Inference using Bidirectional LSTM model and Inner-Attention

#### note:
&emsp;&emsp;在对sentence进行embedding时，当前sentence各个step emit的vector（使用biLSTM生成）能考虑、根据该sentence itself的信息进行加权，故称为inner-attention，该想法的根据是：when human read one sentence, people usually can roughly form an intuition about which part of the sentence is more important according past experience.

#### comment：
  1. 实验较少，sentence itself信息计算只实验了mean pooling的情况，对比下max pooling应该更好；或引入tfidf进行加权，因为paper既然提到了不同词的重要性，那也可以跟tfidf做个对比；
  2. differenting input算是一个tricky。在预处理中，将premise和hypothesis共有的word从两边剔除，而且还能加快计算速度。

#### highlight:
&emsp;&emsp;Differentiating input strategy forces the model to focus on different part of the two sentences which may help the classification for Neutral and Contradiction examples as we observed that our model tended to assign unconfident instances to Entailment.
  
#### question:
&emsp;&emsp;有了双向LSTM还需要inner attention？BiLSTM主要考虑了前后文、长文本信息，但是并没有考虑前后文中哪些词重要哪些词不重要。
