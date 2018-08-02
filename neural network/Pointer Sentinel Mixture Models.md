#### note:
　　作者提出了[Pointer Networks](https://github.com/xwzhong/papernote/blob/master/sequence%20to%20sequence/Pointer%20Networks.md)的一种变体。pointer networks仅能使用input text中的词，针对rare word和long-term dependecies，作者提出的pointer sentinel mixture models能结合此前的input和unseen word（相对于input来说的，而不是常指的OOV）。主要步骤如下（文中用于语言模型）：
  1. 使用rnn对句子进行编码，得到前N-1个词的hidden state；
  2. 将第N-1个词的hidden state映射到同hidden size的维度（式2），得到q；
  3. 计算q与前N-1个词的内积（式3），同时计算参数g（由参数s与q计算内积得到），concate两者后进行softmax映射（式7），得到a;
  4. 将a[:vocab_size+1]与对应输入词的one_hot相乘（相当于根据上文得到的附加权重），与原始rnn softmax后的vocab proba distribution相加得到最终的词概率分布。

#### comment:
  1. 该策略能有效上文缓解rare word和长时依赖问题，主要是通过提高上文已出现的词概率来预测当前输出词；
  2. 不完美处是该方法不能生成属于OOV但属于上文中的词；
  3. 文章步骤4讲得不是特别清楚，可以参考[代码](https://github.com/yzh119/Pointer-Sentinel-Mixture-Model/blob/master/src/model.py#L53)进行理解。

#### [code](https://github.com/yzh119/Pointer-Sentinel-Mixture-Model)
