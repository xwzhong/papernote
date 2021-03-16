#### note:
&nbsp;&nbsp;&nbsp;&nbsp;文章提出的DeepFM可以当作[FM](https://github.com/xwzhong/papernote/blob/master/recommender%20system/Factorization%20Machines.md)和[wide&deep](https://github.com/xwzhong/papernote/blob/master/recommender%20system/Wide%20%26%20Deep%20Learning%20for%20Recommender%20Systems.md)的结合版，整体结构如下:
    ![](https://github.com/xwzhong/papernote/blob/master/pic/DeepFM-pic1.png)
    
  + [FM](https://github.com/xwzhong/papernote/blob/master/recommender%20system/Factorization%20Machines.md)：学习低阶特征（单个特征+两个特征交互）
  
    ![](https://github.com/xwzhong/papernote/blob/master/pic/DeepFM-pic2.png)
  + [wird&deep（dnn）](https://github.com/xwzhong/papernote/blob/master/recommender%20system/Wide%20%26%20Deep%20Learning%20for%20Recommender%20Systems.md)：学习多个特征交互的特征

    ![](https://github.com/xwzhong/papernote/blob/master/pic/DeepFM-pic3.png)
#### comment:
  1. 文章主要是实验效果好，同时FM并不是只能学习低阶（≤2的特征交互），它也能泛化到更高阶的交互
  2. word&deep只是手动的引入了一些人工特征，文章并没有用，特别强调似乎有点过

#### more:
  + 文章超参实验结果：
    + 激活函数：relu比tanh效果好
    + dropout：0.9效果最好（以0.1间隔枚举0.5至1）
    + 神经元大小/隐层数：效果先增后减（过拟合）
    + 网络结构：神经元数相同的情况下，递减/相同的方式效果比递增/钻石型效果好
