#### note:
&nbsp;&nbsp;&nbsp;&nbsp;文章是因子分解的经典论文，该策略最重要的是缓解了数据稀疏问题：
  + 背景：某些特征经过关联，与label之间的相关性强，例如，“USA”与“Thanksgiving”、“China”与“Chinese New Year”这样的关联特征，对用户的点击有着正向的影响。换句话说，来自“China”的用户很可能会在“Chinese New Year”有大量的浏览、购买行为，而在“Thanksgiving”却不会有特别的消费行为。
  + 如何解决两个特征之间的组合：一种直接的方法就是采用多项式模型来表示两个特征的组合，x_i为第i个特征的取值，x_i\*x_j表示特征x_i和x_j的特征组合，其系数w_ij即为我们学习的参数，也是x_i\*x_j组合的重要程度
    ![](https://github.com/xwzhong/papernote/blob/master/pic/Factorization%20Machines-pic1.png)
  + 上述方法存在的缺陷：如果第j,k个特征没有在训练集合组合出现，只出现了（i,j）和（i,k）这时将学不到这个特征
  + 文章提出的解决方案：将w_ij拆分为两个向量的点积，得到i和j的向量表示，从而能得到j,k共现时的权重

#### more:
  1. 文章提出的方案不仅缓解数据稀疏问题，还具有更广的适应性（可用于分类/回归/排序），同时优化参数的方式相同（不像svd++等需要专门设计）
  2. [CTR预估模型FM、FFM、DeepFM](https://www.biaodianfu.com/ctr-fm-ffm-deepfm.html#FM%E6%A8%A1%E5%9E%8B%E5%8E%9F%E7%90%86)
  3. idea看着很简单，但是也从理论上解释了为什么类似word embedding方式的好处
