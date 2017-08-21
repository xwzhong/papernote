### How to Construct Deep Recurrent Neural Networks

#### note:
&emsp;&emsp;paper指出了如何构建深层RNN结构的方向，paper逻辑大致如下：

  1. 为什么要构建deep rnn？hypothesis：Deep learning is built around a hypothesis that a deep, hierarchical model can be exponentially more efficient at representing some functions than a shallow one (Bengio, 2009)；
  2. 构建的方向是什么？从以下三个方向加深rnn：input-to-hidden，hidden-to-hidden，hidden-to-output；
  3. 实验。从实验结果来看，shortcut挺好用，但是容易过拟合。

#### comment：
  1. 如何区分模型“复杂”和“有效”？“有效”猜想：用尽可能少的参数达到目的，而不是畸形的。
  2. 关于模型结构、参数大小、过拟合的思考:

        a. 首先针对待解决的问题，设计出合适的DNN结构，比如针对语言模型，可以使用纯RNN，GRU，LSTM等，一般情况下，初期仅考虑准确率情况下，在候选结构中，尽量选取在参数不用非常大的情况下，其结果仍非常好的模型，比如GRU就明显比RNN要好，因为参数大小相同的情况下，GRU明显比RNN更具长时记忆。
        
        b. 适当提高参数大小。设置参数时，考虑选取128,256,512等2的n次方，有利于加快使用GPU的计算。还有神经元参数初始化（使用normalization initialization），learning rate，learning rate decay选取等。
        
        c. 当参数过大时，容易过拟合，此时可以考虑引入dropout、l2正则等，对于word embedding还可以考虑使用adversarial/virtual training，这两种都是非常不错的正则化方式。
  
  3. deep不是目的，解决问题才是。
  
#### highlight:
&emsp;&emsp;stacked RNN：The goal of a such model is to encourage each recurrent level to operate at a different timescale.
