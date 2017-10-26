### Empirical Evaluation of Gated Recurrent Neural Networks on Sequence Modeling
#### note:
  
1. 总体来讲，GRU和LSTM比传统的RNN好;
2. 在学习能力上，GRU不一定输给LSTM，在某些数据集上，参数数目相近的情况下，GRU略胜一筹;
3. 在时间效率方面，如果GRU解决当前问题情况下优于LSTM，那么同时刻下，GRU会比LSTM学习得更充分，反之亦然。

#### comment:
  
1. 对比RNN，GRU和LSTM三者之间学习能力、时间效率时，考虑了参数数目的影响，思考比较严谨，这点不错;
2. 在非常细致的问题优化中再考虑RNN变体的选择，因为就算RNN和LSTM对同一个问题有不同的结果，但是在参数数目相近的情况，其结果差距一般不会太大。

#### [code](https://github.com/jych/librnn)
