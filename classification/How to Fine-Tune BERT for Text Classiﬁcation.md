
#### note:
&nbsp;&nbsp;&nbsp;&nbsp;针对bert在文本分类中的应用，作者尝试了不同的微调方式来评测bert的效果，主要分三大类。
  + 1. Fine-Tuning Strategies 
    + 1.1. 长文本（大于512个token）
      + a. 方式：取前510个tokens、取后510个tokens、取前128+后382个tokens、层级方法（将文本切分成L/510块，并将最后一层的[CLS]输出进行整合）
      + b. 结论：在IMDb and Sogou数据集上都是head+tail表现最好
      
      ![](https://github.com/xwzhong/papernote/blob/master/pic/HowtoFine-TuneBERTforTextClassi%EF%AC%81cation-1.png)
    + 1.2. 不同层的输出
      + a. 方式：使用不同层[CLS]的输出进行映射
      + b. 结论：在IMDb数据上最后一层的输出，以及Last 4 layer+max表现最好
      ![](https://github.com/xwzhong/papernote/blob/master/pic/HowtoFine-TuneBERTforTextClassi%EF%AC%81cation-2.png)
    + 1.3. 信息遗忘和学习率衰退（学习率的大小）
      + a. 方式：调节学习率的初始值
      + b. 结论：学习率过高容易将bert预训练学习到的内容遗忘
      ![](https://github.com/xwzhong/papernote/blob/master/pic/HowtoFine-TuneBERTforTextClassi%EF%AC%81cation-3.png)
      ![](https://github.com/xwzhong/papernote/blob/master/pic/HowtoFine-TuneBERTforTextClassi%EF%AC%81cation-4.png)
  + 2. Further Pretraining
    + 2.1. 具体任务数据再预训练
    + 2.2. 同领域数据再预训练
    + 2.3. 结论：同领域的数据对具体任务更有帮助，其他领域的数据甚至可能起到反作用
    ![](https://github.com/xwzhong/papernote/blob/master/pic/HowtoFine-TuneBERTforTextClassi%EF%AC%81cation-5.png)
    ![](https://github.com/xwzhong/papernote/blob/master/pic/HowtoFine-TuneBERTforTextClassi%EF%AC%81cation-6.png)
    ![](https://github.com/xwzhong/papernote/blob/master/pic/HowtoFine-TuneBERTforTextClassi%EF%AC%81cation-7.png)
  + 3. Multi-task Fine-Tuning
    + a. 方式：用不同数据集微调后再用特定任务数据集微调
    + b. 结论：效果有提升，但是没特别明显
    
    ![](https://github.com/xwzhong/papernote/blob/master/pic/HowtoFine-TuneBERTforTextClassi%EF%AC%81cation-8.png)
  + 4. Few-ShotLearning
    + a. 方式：使用不同百分比的数据进行微调
    + b. 结论：随着微调数据集郑家，error rate越来越低
    
    ![](https://github.com/xwzhong/papernote/blob/master/pic/HowtoFine-TuneBERTforTextClassi%EF%AC%81cation-9.png)

#### comment:
  + 1. 文章是一篇实验性的文章，把bert尽可能的微调方式都列举了，总的来讲效果比较好的方式是：
    + 长文本仍需要进行实验才能确定是用head，tail还是head+tail，这个跟具体的任务特点相关
    + 但从准确率来看，一般选择最后一层[CLS]的输出，但如果要考虑线上的时间效率问题，则可以使用中间层输出，个人在其他任务中也发现，随着[CLS]层数的增加，准确率确实不断往上增，但时间复杂度也如此
    + 如果具体任务内的无标注数足够多，则用其再预训练，如果不多，则可利用领域内的数据，同时输出中间结果，并进行具体任务的微调测试
  + 2. 目前GLUE数据集上超越BERT的结果主要bert+multi task结果，文章的一些实验可能还不算完备

#### more:
  1. [GLUE leaderboard](https://gluebenchmark.com/leaderboard)
