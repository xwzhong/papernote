#### note:

&emsp;&emsp;paper指出,在使用naive bayes和SVM时,模型结果容易受到model variant, features和数据集的影响.作者通过对NB和SVM实验,得到以下结论:

  1. the inclusion of word bigram features gives consistent gains on sentiment analysis tasks;(原文对情感和主题数据集进行了实验,发现同一个分类器,在情感数据使用了bigram其效果都比unigram好,但在主题分类任务中,有些模型的效果反倒变差.另外,实验没用其它领域的数据)
  2. for short snippet sentiment tasks, NB actually does better than SVMs (while for longer documents the opposite result holds);(此处short snippet数据平均长度为20,最小平均长度为3,最大为24,longer documents指平均长度以百来记,情感数据集中,最小平均长度为231,最大为787)
  3. a simple but novel SVM variant using NB log-count ratios as feature values consistently performs well across tasks and datasets.(NB log-count的计算公式见原文式2)

#### comment:
  1. 原文提出的改进方法简洁,而且运算速度快;
  2. Multinomial Naive Bayes (MNB)在scikit-learn中有实现;
  3. 情感分类中,bigram比unigram好的原因: 在情感类文本中,往往会有否定词,eg:不/喜欢,此时bigram比unigram更能描述文本,换句话讲:bigram学到部分语序信息.
  
#### code:
  1. [作者提供的matlab代码](https://github.com/sidaw/nbsvm)
  2. [个人推荐的python代码](https://github.com/mesnilgr/nbsvm)
