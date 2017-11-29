### Adding Gradient Noise Improves Learning for Very Deep Networks

#### note:
&emsp;&emsp;paper指出,在"very deep"网络中,可以对梯度增加noise,以提高学习的准确率.操作的方法很简单,在每一个step中,对计算得到的梯度添加一个高斯噪音,该高斯分布均值为0,方差随训练步数递减(详见式1).paper从几个的模型(eg:deep fully connected networks, end2end memory networks, neural programmer, neural random access machines, neural GPUs)的实验中论证了该方法的可行性.

#### comment:
  1. 针对deep fully connected networks, 该方法有以下好处: 
  
   * a. 即使没有gradient clipping操作,该方法仍表现优异.
   * b. 对参数初始化不敏感.

  2. 论文提出的trick很简单,但是该方法适用于深层(复杂)的网络结构,用于shallow网络反倒可能使效果变差.
  3. 在引入noise时,考虑了模型在收敛时最佳梯度不断变小的情况,因此将step作为noise的参数,同时,对于一般的随机因子,高斯分布是个不错的选择.
  4. noise在我们的观念中都是应该剔除的,但是有些实验表明,对pure数据添加适当的噪音能提高模型准确率,特别是针对容易过拟合的模型,此处noise起到的作用是防止过拟合.同时也有curriculum learning方式指出,应该尽可能得将这种tough(包含noise)样本尽可能地在后期学习(或者剔除).这两种思路都没错,但是都有其适用的前提.
  5. 由引入noise能提升效果可知,neural networks模型在训练过程中仍有很多不定性,如果是确定的,应该就不会引入不确定的变量.

#### highlight:
&emsp;&emsp;We found that adding noise to the gradient during training helps training and generalization of complicated neural networks. We suspect that the effects are pronounced for complex models because they have many local minima.
