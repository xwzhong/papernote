#### note:
&nbsp;&nbsp;&nbsp;&nbsp;旧不同特征之间的关联问题，文章提出使用cross network进一步的增强特征之间的交互，deep&cross结构如下：
    ![](https://github.com/xwzhong/papernote/blob/master/pic/Deep%20%26%20Cross%20Network%20for%20Ad%20Click%20Predictions-pic1.png)
  + deep network：标准的前馈神经网络
  + cross network：第k层的输出为第0层和第k-1层输出交互得到，相当于第0层经过多次特征交互后计算得到的加权输出：
    ![](https://github.com/xwzhong/papernote/blob/master/pic/Deep%20%26%20Cross%20Network%20for%20Ad%20Click%20Predictions-pic2.png)
  + 实验：对比了在同参数量下dnn vs dcn的效果，或同loss下dnn vs dcn需要的参数量，实验相对严谨：
    ![](https://github.com/xwzhong/papernote/blob/master/pic/Deep%20%26%20Cross%20Network%20for%20Ad%20Click%20Predictions-pic3.png)
    
    ![](https://github.com/xwzhong/papernote/blob/master/pic/Deep%20%26%20Cross%20Network%20for%20Ad%20Click%20Predictions-pic4.png)

#### comment:
  1. 文章虽然提出cross network公式看起来很漂亮，解释起来有一定的可行性，但是实际带来的收益却比较小，以fig3的logloss下降为例，2layers+32nodes的logloss相对下降0.4%，而实验没有用测试集的auc等直接指标，可能也是因为效果不明显（虽然论文说an improvement of 0.001 in logloss is considered as
practically significant，但个人不买单）
