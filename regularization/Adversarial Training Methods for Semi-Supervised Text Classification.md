### Adversarial Training Methods for Semi-Supervised Text Classification

#### note:
&emsp;&emsp;paper提出使用adversarial training和virtual adversarial training方式运用于文本分类中，此前已有相关paper证明，adversarial training和virtual adversarial training在图像分类方面已有很出色的表现。提出的原理在于，如果测试语料中有很小的perturbation，训练出来的model仍可能在测试中轻易判错（可见[样例](https://blog.openai.com/adversarial-example-research/))。在用于文本中时，其运用步骤大致如下：
  
  1. 使用word embedding。原因在于离散变量难以实现无穷小的计算，而连续型变量，每增加一点都是有意义的。
  2. 根据词频进行标准化。类似与z-score。
  3. 引入perturbation（干扰项）——adversarial training和virtual adversarial training。
  
   + a. adv的思想：使用loss来计算embedding接下来最可能的变化方向；
   + b. vat的思想：尽可能使model的分界面光滑。

#### comment:
  1. 步骤2中进行了标准化操作，其中一点是考虑了参数初始化的影响——embedding的某些元素可能特别大，而激活函数的值域一般是(-1, 1)或(0, 1), 为了加快收敛，会尽可能将初始化参数后的激活值限定在中间部分（0或0.5)。
  2. 该paper提出引入文本中的对抗学习，可用于各种各样的文本类型任务中，虽然简单，但是理论很深，而且从实验结果来看，效果非常不错。
  3. [adversarial training笔记](https://github.com/xwzhong/papernote/blob/master/regularization/Explaining%20and%20Harnessing%20Adversarial%20Examples.md)、[virtual adversarial training笔记](https://github.com/xwzhong/papernote/blob/master/regularization/Distributional%20Smoothing%20with%20Virtual%20Adversarial%20Training.md)

#### highlight:
&emsp;&emsp;Adversarial training (Goodfellow et al., 2015) is a novel regularization method for classifiers to improve robustness to small, approximately **worst** case perturbations.


### more reading:
[note](https://github.com/dennybritz/deeplearning-papernotes/blob/master/notes/adversarial-text-classification.md)
