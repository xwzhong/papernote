### Noise-Contrastive Estimation for Answer Selection with Deep Neural Networks

#### note:
&emsp;&emsp;paper指出，在answer selection中将classification问题转为ranking问题（此前已有相关paper是这样做的，eg：QA-LSTM），同时对三种负样本的sample方式进行了实验比较：

  1. Random Sampling. We randomly select a number of negative samples for each positive answer.
  2. Max Sampling. We select the most difficult negative samples. In each epoch, we compute the similarities between all (p+, p−) pairs using the trained model from the previous training epoch. Then we select the negative answers by maximizing their similarities to the positive answer.
  3. Mix Sampling. We take advantages of both random sampling and max sampling by selecting half of the samples from each strategy.

#### comment：
&emsp;&emsp;此处提出的max sampling策略想法不错，利用上一个epoch最可能降低accuracy的负样本进一步训练，有点对抗的意味，而且实验结果也不错。

#### [code](https://github.com/castorini/NCE-CNN-Torch)
