#### note:
　　DropConnect是传统dropout上的改进，相比于深度学习中使用的Dropout，在理论上更具泛化能力。以某神经元为对象，Dropout对该神经元的输出进行调整（添加mask，共需调整1个元素），而DropConnect则对该神经元的输入进行调整（添加mask，共需调整k个元素，k代表该神经元所在位置上一层的输出维度）。
  
#### comment:
  1. 截止2018-06-29，Google搜索显示该论文引用达到935，但在NLP领域看到使用的不多，存疑。

#### code:
  1. [DropConnect Implementation in Python and TensorFlow](https://nickcdryan.com/2017/06/13/dropconnect-implementation-in-python-and-tensorflow/)
  2. [Can I use `tf.nn.dropout` to implement DropConnect?](https://stackoverflow.com/questions/44355229/can-i-use-tf-nn-dropout-to-implement-dropconnect)

#### more:
  1. [Regularization of Neural Networks using DropConnect](https://cs.nyu.edu/~wanli/dropc/)
  2. [Difference between DropOut and DropConnect](https://stats.stackexchange.com/questions/201569/difference-between-dropout-and-dropconnect)
  3. [What is the difference between dropout and dropconnect?](https://www.quora.com/What-is-the-difference-between-dropout-and-dropconnect)
  4. [Deep learning：四十六(DropConnect简单理解)](https://www.cnblogs.com/tornadomeet/p/3430312.html)
