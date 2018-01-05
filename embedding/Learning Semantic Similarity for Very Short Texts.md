#### note:
&emsp;&emsp;文章立足与短文本(实验使用了长度为10, 20和30的句子)语义相似度匹配, 分析了从词向量到句向量的不同整合方式,eg: 对每个维度取min,max,min/max拼接,mean,与idf结合等策略,最终提出了一个有监督的权重学习模型.

#### comment:
  1. 经实验发现以下特征:

      + a. 使用单纯的tf-idf向量匹配,文本越长,匹配错误率越低(length_10_36.15%-length_20_20.09%-length_30_12.55%);
      + b. 对于长文本(实验中,长度为30),paper实验的各种整合方式对其错误率的影响相对较小(±4%)vs(±12.8)length10;
      + c. 在无监督的方式中, mean+idf weighted的方式在长度为10和20的匹配中表现优异,效果比较:10>20>30;
      + d. 在长度为20的文本比较distance计算公式, split error指标中,Mean+Euclidean比Mean+cosine高1.5%;
      + e. 在有监督的权重学习中,长度为20的文本其split eror为14.44%,比mean+idf weighted+cosine低1.33%;
  2. paper提出的有监督学习importance factors方案给人眼前一亮,比较可惜的是没在长度为10的文本中进行实验;
  3. 在importance factors策略中,在学习到的权重基础上乘上idf值效果会不会更好?因为importance factors仅学习到不同词之间的相对权重,没有考虑词本身的重要性;

#### highlight:
  1. Our main contribution is a first step towards a hybrid method that combines the strength of dense distributed representations— as opposed to sparse term matching—with the strength of tf-idf based methods to automatically reduce the impact of less informative terms.
  2. In this paper, we show how word embeddings can be combined into a new vector representation for the entire considered fragment, in which the impact of frequent words, i.e. with a low idf-component, and therefore mostly non-informative—is reduced with respect to more informative words. This leads to a significant increase in the effectiveness of detecting semantically similar shorttext fragments, compared to traditional tf-idf techniques or simple heuristic methods to combine word embeddings.
  3. We regard two text fragments to be semantically similar if their corresponding vector representations lie close to each other according to some distance measure, and dissimilar if the vectors lie farther apart.(paper给出的语义相似度定义)
