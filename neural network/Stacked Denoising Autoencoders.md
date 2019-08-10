#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper提出“栈式降噪自编码”算法提取高级特征，演变过程如下：
  + a. 自编码算法。神经网络只含一个隐层（一般hidden size比输入维度小），输入和输出相等，loss即为输入和输出的差异，训练好隐层即对应高级特征，然后再结合具体的场景微调模型。结构图如下：
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Stacked_Denoising_Autoencoders_autoencoders.PNG)
  + b. 降噪自编码算法。在自编码算法的基础上，输入中的元素以一定的概率置为0（输出不变），使得模型在输入数据corrupt（损坏）的情况下仍能复原，提高抗噪声能力，同时在一定程度上减轻了训练数据与测试数据的代沟。
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Stacked_Denoising_Autoencoders_denoising_autoencoders.PNG)
  + c. 栈式降噪自编码。常规的自编码算法只含有一个隐层，通过栈式叠加，当训练好第k层隐层的参数后，固定1到k层的隐层参数，训练第k+1层的参数，最后再根据具体任务微调，结构图如下：
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Stacked_Denoising_Autoencoders_stacked_denoising_autoencoders.png)


#### comment:
  + a. “降噪”跟常规的dropout类似；
  + b. 栈式自编码算法看起来像是逐层获取更高级编码特征。
  + c. 单隐层不是可以拟合任意函数，为什么还要栈式自编码：
      + 输入的向量维度一般比hidden size高
      + 单隐层虽然能编码任意的表达式，但是深层网络往往更简洁（此处是不是应该有理论或实验证明？？）
  + d. [深层网络拟合能力强，为什么还要自编码？](https://blog.csdn.net/aisikaov5/article/details/51193137)数据获取问题、局部极值问题、过拟合、梯度弥散问题。


#### more:
  + a. [堆叠降噪自动编码器 Stacked Denoising Auto Encoder（SDAE）](https://blog.csdn.net/zbzcDZF/article/details/86570761)
  + b. [Deep Learning 学习笔记（8）：自编码器( Autoencoders )](https://www.cnblogs.com/Ponys/p/3315642.html)
  + c. [栈式自编码算法](https://blog.csdn.net/aisikaov5/article/details/51193137)