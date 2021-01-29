#### note:
&nbsp;&nbsp;&nbsp;&nbsp;文章是典型的双塔结构——分别对content和user编码得到一个向量，然后根据两个向量的cosine值来衡量相似度，要点记录：
  + a. content和user向量使用pair-wise相似度计算的原因（而不是用交互式，比如concat/element-wise multiplication后映射到一个浮点值）：the pair-wise calculation is more similar to the matrix factorization method that can provide high-level user and item factors（个人感觉这种说法本身没有错，但是不能很好的解释为什么不用fusion方式——用不用fusion应该从最终的效果出发）
  + b. 计算pair的score时使用cosine而不是dot product：文章只说测试效果发现cosine比较好，但是没有给出理论分析
  + c. loss设计使用了max-margin loss而不是softmax function with categorical cross-entropy：文章也是说实验效果margin更好，也没给出理论解释
  + d. margin-loss引入了grid-searched：the number of negative samples as 20 and the margin value ∆ as 0.2
  ![](https://github.com/xwzhong/papernote/blob/master/pic/Deep%20Content-User%20Embedding%20Model%20for%20Music%20Recommendation.png)
  
#### comment:
  1. paper比较基础，偏实验性，理论解释较少
