#### note:
&emsp;&emsp;paper提出了一种结合"检索+seq2seq"的对话模型,整体思路是,先使用bm25检索post,得到最可能的k个问答对,然后再用seq2seq训练得到的生成模型对k个问答对进行重新排序,其主要步骤如下:
  1. First, we use the IR model to retrieve a set of k candidate QA pairs(k = 10);
  2. Second, we pair q with each candidate answer ri and calculate a confidence score o(ri) = s(q, ri) for each pair using the scoring function in Eqn. 2 of the rerank model;
  3. Third, we consider the answer r with the maximal score o(r) = max o(ri): if o(r) ≥ T, take the answer r; otherwise output a reply r 0 from the generation based model;
  

#### comment:
  1. 文中对比了seq2seq是否加入attention机制,经实验,加了attention机制的模型表现更优;
  2. 使用seq2seq训练得到的模型对检索得到的问答对进行重排,这点比较新颖,能表达数据更细致的信息,但是仍未避免seq2seq用于生成对话内容时的缺陷(通用性回复多,句子偏短等), 只是将出现这种类型的回复比例降低了;
  3. 实验给出的最高评分(suitable数+neutral数占总回复比)为60.01%.

#### more reading:
&emsp;&emsp;[揭秘阿里小蜜：基于检索模型和生成模型相结合的聊天引擎](http://blog.csdn.net/uwr44uouqcnsuqb60zk2/article/details/78849003)
