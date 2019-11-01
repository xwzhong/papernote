#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper在bert基础上引入多任务学习，与原bert相比，在GLUE数据集上高2.2%绝对值，引入多任务策略比较简单：当前step，随机选择某个任务，然后在预训练的bert基础上微调任务相关（包含bert本身）参数。

#### comment:
  + 1. 文章idea根源：借助不同任务学习到不同的能力在bert参数部分（不同任务共享的参数）得到展现；
  + 2. 不同任务在直接如论文方式微调情况下也可能阻碍其它任务的学习。

#### more:
  1. [官方提供的pytorch代码](https://github.com/namisan/mt-dnn)
