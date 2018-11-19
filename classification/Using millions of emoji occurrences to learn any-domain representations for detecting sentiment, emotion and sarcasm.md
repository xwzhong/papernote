#### note:
　　针对sentiment、emotion和sarcasm任务，paper提出使用emoji标注的大量数据下pretrain后进行transfer learning，要点如下：
  1. pretrain。使用Twitter含有指定emoji集合（64个emoji）的数据，以emoji为类别标签训练分类器（一个训练样本只有一个标签、一条text可能有多个标签-分多条训练样本）。
  2. model architecture。embedding-bilstm-attention sum+skip connection-softmax。
  3. transfer learning-chain thaw。使用2中的model architecture预训练好模型后，使用target task对pretrain好的参数进行fine-tuning，提出了chain thaw策略——先更新最后一层参数，然后再从最低层依次往上更新其参数，其中使用了valid data来判断训练是否结束。

#### comment:
  1. 模型效果好的原因探索：
  + a. pretrain数据量大。64 emoji就有12.4亿数据量，单个emoji数据量最少为510w+，最多为2.3亿，相差40+倍（为了平衡数据需要做平衡操作-文章使用了upsampling）；
  + b. 模型结构设计。使用了attention机制和skip connection策略，在transfer learning时，使用了chain thaw策略，该方法在NER中也能提升1%的F1值。
  2. paper中绘制的fig6有很大用处：
  + a. 使用无监督方式自动区分情感类别；
  + b. 描述不同情感之间的距离；
  + c. 可将emoji归为不同的大类。
  3. 不足之处是因使用了bilstm训练时间较长，或许使用embdding-position encoding-attention sum+skip connection-softmax也能达到与使用bilstm相近的效果，同时明显提升时间效率。
  4. 文章3.2部分提到对embedding加constrain，使其值映射到[-1, 1]，估计是为了后续skip connection部分平齐数值范围而添加。
  
#### more:
  1. [论文主页](https://www.media.mit.edu/projects/deepmoji/overview/)
  2. [code](https://github.com/bfelbo/deepmoji)
  3. [pretrain的结果体验](http://deepmoji.mit.edu)
  4. [用python-pandas作图矩阵](https://www.jianshu.com/p/47b54eb35eed)
  5. [SciPy Hierarchical Clustering and Dendrogram Tutorial](https://joernhees.de/blog/2015/08/26/scipy-hierarchical-clustering-and-dendrogram-tutorial/#Perform-the-Hierarchical-Clustering)
  6. [How to Handle Imbalanced Classes in Machine Learning](https://elitedatascience.com/imbalanced-classes)
  7. [undersampling和oversampling进行训练和测试时的注意点](https://www.marcoaltini.com/blog/dealing-with-imbalanced-data-undersampling-oversampling-and-proper-cross-validation)
  8. [这个围笑代表什么 可能麻省理工的AI比你更懂](http://www.qingpingshan.com/m/view.php?aid=310874)
