#### note:
&nbsp;&nbsp;&nbsp;&nbsp;针对参数共享的多任务学习，文章引入expert的概念，不同expert学习不同的知识，再通过gate来控制不同expert提供知识的多少，文章提出路径：
  + 背景：常见的multi task是共享底层网络的（Shared-Bottom model），结构如下图（缺点：不同的任务可能关联性差，直接将不同任务的主要参数进行共享，如果不同任务的关联性比较低，模型不容易在两者中都拟合的特别好，跟模型的学习能力相关）：
    ![](https://github.com/xwzhong/papernote/blob/master/pic/Modeling%20Task%20Relationships%20in%20Multi-task%20Learning%20with%20Multi-gate%20Mixture-of-Experts-pic1.png)
  + 改进思路：将共享的参数拆分成多组，每一组相当于一个expert，用以学习特定方面的知识，然后通过gate来控制每个expert对不同任务加权，结构图：
    
    ![](https://github.com/xwzhong/papernote/blob/master/pic/Modeling%20Task%20Relationships%20in%20Multi-task%20Learning%20with%20Multi-gate%20Mixture-of-Experts-pic2.png)
  + 进一步升级：n个任务引入n组gate，原来单gate中，gate参数相同（可以理解为attention参数相同，输入不同），结构图：
    ![](https://github.com/xwzhong/papernote/blob/master/pic/Modeling%20Task%20Relationships%20in%20Multi-task%20Learning%20with%20Multi-gate%20Mixture-of-Experts-pic3.png)

#### comment:
  1. paper主要想解决不同任务关联性低时参数学习存在一定冲突问题，通过引入多组参数+gate控制的想法来解决，学习的目标是两个任务的预测效果都要求比较好

#### more:
  1. [多任务学习模型详解：Multi-gate Mixture-of-Experts（MMoE ，Google，KDD2018）](https://blog.csdn.net/ty44111144ty/article/details/99068255)
