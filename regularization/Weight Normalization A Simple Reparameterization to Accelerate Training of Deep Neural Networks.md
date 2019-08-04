### Weight Normalization: A Simple Reparameterization to Accelerate Training of Deep Neural Networks

#### note:
&emsp;&emsp;paper以batch normalization为基础，提出了weight normalization。针对f(x)=wx+b，BN对x进行了normalization操作，而WN则对w进行调整，具体操作是令w的“值”和“方向”分别用不同参数表示，从而减少“值”与“方向”之间的依赖。

#### comment：
1. 与BN相比，WN排除了同个batch中sample与sample之间的依赖关系，同时也解决了BN batch设置需较大，training和infering存在差异的问题；
2. 缺点，模型参数需专门初始化；
3. 从f(x)=wx+b中x的角度解释WN，经过WN，x的均值为0，方差为||v||。（v包含了w的方向信息）

#### highlight:
1. we now have ||w|| = g, independent of the parameters v. We therefore call this reparameterizaton weight normalization.
2. By decoupling the norm of the weight vector (g) from the direction of the weight vector (v/||v||), we speed up convergence of our stochastic gradient descent optimization, as we show experimentally in section 5.
