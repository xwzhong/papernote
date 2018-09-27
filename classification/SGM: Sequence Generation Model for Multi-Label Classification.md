#### note:
　　作者将multi-label classification任务转化为序列生成形式，本文使用了seq2seq with attention结构，encoder对句子进行编码，decoder对各类别进行解码生成。作者所做主要改动如下：
  + a. 在decoder生成第k个label时，如果前k-1步已经出现过了，则对其进行惩罚。（在实操中，具体惩不惩罚需要以实际需求为准）；
  + b. 提出了general embedding。在decoder阶段，生成第k个label不是仅仅考虑k-1步中最高概率的label，作者还考虑了其它label的概率，主要是避免过分依赖最大概率label造成错误累加。

#### comment:
  + a. 作者对模型的改动不算大，亮点是将多标签分类问题转为序列生成，而使用序列生成能很好的学习不同标签之间的关系；
  + b. 如果标签顺序并不是非常重要，使用transformer效果是不是会更好?（transformer对语序的学习能力相对lstm较差）

#### more:
  [深度学习：如何在多标签分类问题中考虑标签间的相关性？](https://zhuanlan.zhihu.com/p/39535198)

#### highlight:
　　The proposed sequence generation model generates labels sequentially and predicts the next label conditioned on its previously predicted labels. Therefore, it is likely that we would get a succession of wrong label predictions in the following time steps if the prediction is wrong at time-step t, which is also called exposure bias.
