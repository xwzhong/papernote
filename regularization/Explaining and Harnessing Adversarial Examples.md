### Explaining and Harnessing Adversarial Examples

#### note:
&emsp;&emsp;paper主要是想解决adversarial样本在训练好的中容易被错分的情况。
  
  1. 作者指出，adversarial干扰主要是由样本的线性特征造成的（文中指出，早期学者已经做出定量分析），因此提出在样本中预先引入这个perturbation（详见paper第3、4部分）；
  2. “样本的线性干扰因子”的计算方式。在当前loss下，样本输入的特征x线性变化方向的该变量，当x第i个特征在当前loss导数下为正时，则说明该特征有变大的可能性，原特征加上这个变化的可能性便可得到adversarial loss。

#### comment:
  1. 不仅是从行文还是所提模型背后的哲理，都值得深究；
  2. 关于计算量。因为需要再从loss反馈到x中，估计需增加一倍左右的计算；
  3. 讨论：train和eval存在鸿沟的原因。现有的训练数据都是有一定的干扰噪音，致使模型并没有学到groundtruth，从而也导致了训练error与测试error之间存在一低一高的问题。引用原文的话是：even those that obtain excellent performance on the test set, are not learning the true underlying concepts that determine the correct output label
  4. 不仅可以用于图像中，还可用于文本中。

#### highlight:
&emsp;&emsp;The adversarial training procedure can be seen as minimizing the worst case error when the data is perturbed by an adversary.

#### more reading:
[深度学习：简单而有局限性的求解方式](https://www.jiqizhixin.com/articles/3e949ae2-48ac-4606-98a0-844fb291c4d4)
