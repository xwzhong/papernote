#### note：
&emsp;&emsp;文章分析了激活函数和参数初始化对neural network的影响，要点如下：

 1. the logistic sigmoid activation is unsuited for deep networks with random initialization because of its mean value, which can drive especially the top hidden layer into saturation. 详见论文3.1部分的分析。
 2. We find that a new non-linearity that saturates less can often be beneficial.
 3. propose a new initialization scheme that brings substantially faster convergence.

#### comment:
 1. Two things we want to avoid and that can be revealed from the evolution of activations is excessive saturation of activation functions on one hand (then gradients will not propagate well，因为在饱和点处的梯度很低，通过前面的layer通过后向反馈得到的信息特别少), and overly linear units (they will not compute something interesting???).
 2. sigmoid函数因均值不是0而造成效果差的原因分析。We hypothesize that this behavior is due to the combination of random initialization and the fact that an hidden unit output of 0 corresponds to a saturated sigmoid.
 3. 对称的激活函数（eg：tanh）与sigmoid函数对比。In the case of symmetric activation functions like the hyperbolic tangent and the softsign, sitting around 0 is good because it allows gradients to flow backwards. However, pushing the sigmoid outputs to 0 would bring them into a saturation regime which would prevent gradients to flow backward and prevent the lower layers from learning useful features。在y≈0处，sigmoid接近饱和，而以tanh为例，此时x≈0，此处的梯度大，有利于最后一层的梯度信息传递给前面隐层。从以上分析中也可以发现，在选用对称激活函数时，初始化策略一定要关于0对称，作者还从理论角度分析，给出了常用的glorot初始化策略，详见式16；
 4. 为什么使用交叉熵代替二次代价函数——在饱和状态，二次代价函数的梯度小，导致参数偏导降低，减缓学习速率，而交叉熵因约去了梯度，进而学习速率教高，详见[文章](http://blog.csdn.net/yqljxr/article/details/52075053)；而文中也提到，交叉熵代价函数其平滑的面更少（详见4.1，fig5）。
 5. pretrain在实践中可多做思考。Note that deep networks with sigmoids but initialized from unsupervised pre-training (e.g. from RBMs) do not suffer from this saturation behavior.

#### conclusions from paper：
 1. The more classical neural networks with sigmoid or hyperbolic tangent units and standard initialization fare rather poorly, converging more slowly and apparently towards ultimately poorer local minima.（因此建议结合tanh激活函数和glorot初始化策略）
 2. The softsign networks seem to be more robust to the initialization procedure than the tanh networks, presumably because of their gentler non-linearity.（绘制tanh和softsign曲线可知，tanh随x变化更剧烈）
 3. For tanh networks, the proposed normalized initialization can be quite helpful, presumably because the layer-to-layer transformations maintain magnitudes of activations (flowing upward) and gradients (flowing backward).
 4. Monitoring activations and gradients across layers and training iterations is a powerful investigative tool for understanding training difficulties in deep nets.
 5. Sigmoid activations (not symmetric around 0) should be avoided when initializing from small random weights, because they yield poor learning dynamics, with initial saturation of the top hidden layer.
 6. Keeping the layer-to-layer transformations such that both activations and gradients flow well (i.e. with a Jacobian around 1) appears helpful, and allows to eliminate a good part of the discrepancy between purely supervised deep networks and ones pre-trained with unsupervised learning.
 7. Many of our observations remain unexplained, suggesting further investigations to better understand gradients and training dynamics in deep architectures.
