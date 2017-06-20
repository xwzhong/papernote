### Exploring Sparsity in Recurrent Neural Networks

#### note:
1. paper想通过“pruning weights"的方式提高rnn在测试时的执行速度，此处提到的pruning weights是通过weights的条件限制，使更多的weight为0，模型变得更sparse，进而加快运算；
2. 在deploy过程中，文中说训练仅增加了一个常量级（根据paper提到的算法，比较可信）；
3. 在测试方面，如果仅以参数中非零个数为变量，同个数下，结果确实是比较好，但是，如果同hidden layer下分为dense和sparse，dense方式的效果更好。文章说测试的准确率比原来的dense方式更优是从非零个数的参数角度考虑的，至于大家批判这种方式是否合理就见仁见智了。

#### comment:
1. 既然sparsity能达到90+%，是不是可考虑直接减小模型的规模？
2. 从某个角度验证了4.17openai发的[paper](https://arxiv.org/abs/1704.05119)思路。

#### practice: 
&emsp;&emsp;这篇文章的改进思路更适合大项目。
