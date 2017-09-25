### Recurrent Dropout without Memory Loss
#### note:
  
&emsp;&emsp;针对RNN、LSTM和GRU具有长时记忆能力，作者提出了在hidden2hidden层间进行dropout的策略，该策略有别于[Recurrent Neural Network Regularization](https://arxiv.org/abs/1409.2329)指出进行dropout的位置，而且经实验发现，paper提出recurrent dropout方式整合input2hidden及hidden2output位置dropout能得到更好的效果。以LSTM为例，在hidden2hidden层，作者仅对“hidden state update”进行dropout（详见式9）。同时dropout方程不同于hinton提出的式3，而为式18。 

#### comment:
  
1. 文章对前人提出在hidden2hidden层进行dropout方式进行比较，实验发现所提出的方法得到的结果最好；
2. paper提出的改进方式，隐约给人一种“Recurrent Neural Network Regularization”论文中的思想，没有直接对context state进行dropout；
3. 从编码的角度看，该方式在tensorflow LSTMCell，GRUCell等很容易添加，仅需几行代码。（tf源码nn_ops.py中实现了式18dropout方程，同时虽然LSTMCell相比BasicLSTMCell添加了很多备选trick，但是并没有实现文中提到的策略）

#### code: 
* [theano](https://github.com/stas-semeniuta/drop-rnn)

#### q&a: 
1. per-step和per-sequence没有完全理解其区别
