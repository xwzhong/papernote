#### note:
&emsp;&emsp;paper对梯度下降可使用的优化算法进行的简要介绍，有以下几个方面：

  1. Gradient descent variants: batch, stochastic及mini-batch gradient descent;
  2. 梯度优化算法：momentum、nesterov accelerated gradient（NAG，momentum的改进版）、adagrad、adadelta、RMSprop、Adam等、同时给出了[可视化链接](http://cs231n.github.io/neural-networks-3/);
  3. 并行化策略；
  4. 简要提及其它优化策略：shuffling and curriculum learning、batch normalization、early stopping、gradient noise；

#### comment:
  1. 一般来讲，我们会选用mini-batch的方式训练，但是不要忘记，算法推导之初是使用batch，限于运行内存/显存、单步更新速率，从而使用了mini-batch，个人实验发现，mini-batch越大，收敛速度越快，如果内存/显存允许，可尽量调高mini-batch数。但也不要忘记对同一个epoch进行shuffle操作，降低同个mini-batch样本与样本间的相互影响；
  2. 梯度优化算法，主要还是针对learning rate的优化，更深入可指每个参数learning rate的优化。从momentum到NAG，再到adagrad、Adam等，可清晰地看到中间演化过程，最终作者也提及，默认可使用Adam优化策略，其用动量的角度引入一阶和二阶梯度。
