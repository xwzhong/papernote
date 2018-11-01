#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper指出使用词语相似度的高阶关系进一步抽取word vector语义信息，具体操作是矩阵相乘（类似于有向图的可达矩阵），同时可将该高阶信息通过线性转化得来；

#### comment：
  1. paper提出的观点有一定的理论依据，想法挺有意思，同时在不同DL模型中引入方便;
  2. 抛开paper提出的改进策略，各项实验都表明fasttext效果优于word2vec和glove,整体排序: fasttext>glove>word2vec;
  3. 相比于fasttext，该策略对word2vec和glove提升比较明显，同时alpha参数选取比较麻烦，alpha选得差会降低模型的效果（综合来看，选用fasttext时训练word embedding时对模型提高有限）；
  

#### more:
  1. [CoNLL 2018 ｜ 最佳论文揭晓：词嵌入获得的信息远比我们想象中的要多得多](https://mbd.baidu.com/newspage/data/landingsuper?context=%7B%22nid%22%3A%22news_8705292014518314824%22%7D&n_type=0&p_from=1)
  2. [code](https://github.com/artetxem/uncovec)
