### Dialog Context Language Modeling with Recurrent Neural Networks

#### note:
&emsp;&emsp;针对language model，paper对dialog level信息的employ进行了总结，从最基本的language model，到多轮对话，值得记录的有以下几点：

1. Single-Turn-RNNLM: Conventional RNNLM that operates on single turn level with no context information;
2. BoW-Context-RNNLM: Contextual RNNLM with BoW representation of preceding text as context;
3. DRNNLM: Contextual RNNLM with turn level context vector connected to initial RNN state of the target turn;
4. CCDCLM: Contextual RNNLM with turn level context vector connected to RNN hidden state of the target turn;
5. DACLM: RNNLM with true dialog act context vector connected to RNN state of the target turn at each time step at each time step;
6. IDCLM: The last RNN state of turn k?1 serves as the starting RNN state of k+1 and the context vector to turn k, which is fed to turn k’s RNN hidden state at ach time step together with the word input;
7. ESIDCLM: under IDCLM, use external RNN to model the context changes explicitly

#### comment:
1. IDCLM考虑了同一个人的“说话风格”；
2. ESIDCLM更像是句子层面的recurrent neural network；
3. 从实验结果来看，仍旧是引入了额外tag信息的DACLM模型表现更优。
