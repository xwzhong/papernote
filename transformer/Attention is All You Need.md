#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper提出transformer，其以encoder-decoder结构对句子进行编码映射:
  1. encoder:  InputEmbedding + PositionalEncoding + N*[LayerNorm(x+MultiHeadAttention(x)) + LayerNorm(x+FeedForward(x))]
  2. decoder: OutputEmbedding + PositionalEncoding + N*[LayerNorm(y+MaskedMultiHeadAttention(y) + LayerNorm(y+MultiHeadAttention(y)) + LayerNorm(y+FeedForward(y))] + Linear + Softmax
  如下图：
![](https://github.com/xwzhong/papernote/blob/master/pic/transformer.png)

  
  各组件详细介绍：
  1. positional encoding(paper3.5）:选用原因——We chose this function because we hypothesized it would allow the model to easily learn to attend by relative positions, since for any fixed offset k, PE_pos+k can be represented as a linear function of PE_pos;
  2. [layer normalization](https://github.com/xwzhong/papernote/blob/master/regularization/Layer%20Normalization.md);
  3. attention, 多个Scaled Dot-Product Attention拼接构成了multi-head attention:

  + a. Scaled Dot-Product Attention(paper3.2.1), 其最后添加scale的原因——We suspect that for large values of dk, the dot products grow large in magnitude, pushing the softmax function into regions where it has extremely small gradients，计算见下图：

  ![](https://github.com/xwzhong/papernote/blob/master/pic/Scaled%20Dot-Product%20Attention.png)
  
  + b. Multi-Head Attention(paper3.2.2). 将V,K,Q进行线性映射，并分别split为num_head，进而对num_head个部分计算Scaled Dot-Product Attention，最后concat并映射，计算见下图：
  
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Multi-Head%20Attention.png)
  
  4. Position-wise Feed-Forward Networks(paper3.3)):FFN(x) = max(0, x*W_1 + b_1)*W_2 + b_2。



#### comment：
  1. transformer核心组件是multi-head attention部分，token向量交叉计算，最后输出加权后的向量，直观上感觉比较简单，但是加上了多个辅助技巧后实验效果确实不错；
  2. transformer结构中使用了很多小技巧，如scale, layer normalization, mask, residual connection, label smoothing等，有些缺乏必要理论解释；
  3. 单个epoch因并行使得训练速度较快，但个人通过一些运用发现，其拟合速度较慢，可能是由于整个网络搜索空间大，致使其需要更多的尝试才能找到收敛方向，同时也预示使用预训练的参数能加快收敛速度。


#### more:
  1. [论文阅读笔记之Attention Is All You Need](https://blog.csdn.net/mrphd/article/details/79357890)
  2. [tensorflow code](https://github.com/Kyubyong/transformer)

#### highlight:
  1. why self attention:One is the total computational complexity per layer. Another is the amount of computation that can be parallelized, as measured by the minimum number of sequential operations required. The third, the shorter these paths between any combination of positions in the input and output sequences, the easier it is to learn long-range dependencies.
  2. Label Smoothing During training, we employed label smoothing of value e_ls = 0.1 [36]. This hurts perplexity, as the model learns to be more unsure, but improves accuracy and BLEU score.
