#### note:
&nbsp;&nbsp;&nbsp;&nbsp;针对推荐系统中“**记忆**”和“**泛化**”问题，文章提出使用“**wide**”和“**deep**”策略构建模型：
  + a. **记忆（wide）**：线性模型中“记住”非线性特征（对于非线性特征，使用交叉乘积变换方式得到one hot特征）
  + b. **泛化（deep）**：针对类别特征，使用低维稠密向量表示，进而泛化未出现组合特征（类似于因式分解，将非线性特征分解成基础因子，线上预测使用这些基础因子组合得到此前少出现的组合特征-非线性特征）
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Wide%20%26%20Deep%20Learning%20for%20Recommender%20Systems.png)

#### more:
  1. ensemble（多个模型单独训练，最后对预测结果进行汇总）：参数不共享，单个模型参数量更多
  2. joint（多模型/模块同时训练，只有一个预测结果）：相对较好，可只对模型薄弱模块增加参数
  3. While Wide & Deep has a slightly higher offline AUC, the impact is more significant on online traffic. One possible reason is that the impressions and labels in offline data sets are fixed, whereas the online system can generate new exploratory recommendations by blending generalization with memorization, and learn from new user responses.
