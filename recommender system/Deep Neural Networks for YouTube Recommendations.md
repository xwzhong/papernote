#### note:
&nbsp;&nbsp;&nbsp;&nbsp;文章介绍了YouTube视频推荐的实现逻辑，整体结构分两部分（candidate generation和ranking）：
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Deep%20Neural%20Networks%20for%20YouTube%20Recommendations-pic1.png)
  
  + candidate generation：目的（粗筛，生成排序的候选集），路径（训练时构建分类任务，线上以向量召回方式使用时），模型结构和各个模块特点依次如下：
 
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Deep%20Neural%20Networks%20for%20YouTube%20Recommendations-pic2.png)

    * 分类标签：正样本（视频观看时长大于特定值），负样本（candidate sampling + importance weighting）【显示的数据（eg：点赞/踩）比较稀疏，而曝光和点击数据又可能因缩略图迷惑性造成虚假点击】
    * 多相特征：连续型（视频上传时长），类别特征（观看过的视频【以id形式编码】，用户搜索的token，地理位置特征等）
    * 标签和上下文选择：构建训练/预测时，以待推荐的时间前信息作为输入，而不是将未来的信息也作为输入
  + ranking：目的（有限的预测耗时内，引入更多特征），路径（构建时长预测回归模型），模型结构和优化点依次如下：

  ![](https://github.com/xwzhong/papernote/blob/master/pic/Deep%20Neural%20Networks%20for%20YouTube%20Recommendations-pic3.png)

    * 特征表示：
        * 特征工程（eg：在这个主题下上一次用户看是多久前）
        * 类别特征（常规编码embedding 方式）：曝光过，点击过的，搜索语言
        * 归一化连续特征：标准化（均值为0，方差为1），次线性（x^0.5），超线性（x^2）【归一化的原因是神经网络对输入数据分布敏感（参考batch normalization），使用次/超线性使增强单个特征的表达丰富度，实验效果loss降低0.2%】
    * 对观看时长建模：正样本（用户有点击），负样本（用户没点击），使用观看时长对正样本score进行加权
    * 模型参数（全连接层）：不同模型参数的实验效果：
    
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Deep%20Neural%20Networks%20for%20YouTube%20Recommendations-pic4.png)

#### more:
  1. The primary role of ranking is to use impression data to specialize and calibrate candidate predictions for the particular user interface.
