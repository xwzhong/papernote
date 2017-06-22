### Generating Long and Diverse Responses with Neural Conversation Models

#### note:
&emsp;&emsp;paper仍旧是想解决使用seq2seq训练chatbot得到的回复具有长度短、通用性回复多的问题；
  1. 解决生成的句子短：在encoder部分引入已生成的response内容，同时因为显存大小的限制，提出了glimpse模型；
  2. 解决通用性回复多：在test/eval部分，第一个timestep随机选取候选word，从第二个timestep开始才使用常规beam search方式进行搜索。

#### comment:
  1. seq2seq中，encoder部分的文本可以尽可能地长，因为encoder部分没有output；相反，decoder部分的output部分需要计算softmax，显存占用明显，特别是上decoder部分的vocabulary非常大的时候，因此paper才提出note1中的glimpse模型；
  2. 文中提到“self attention”，即target side attention是指在训练时，encoder部分加入已生成的内容。这样做是因为the decoder has to keep track of everything output so far in its fixed-lenght hidden state vector, which leads to incoherent or even contradictory。（难道用常见的attention mechanism还不能很好地解决？？）；
  3. 在test/eval部分，第一步随机选取word，该策略可能的前提是有大量的训练语料，把一个post所有可能的回复都尽可能“学习过”(ps:本文用了23亿数据）；
  4. 使用seq2seq做生成式对话，同长度post下，用model生成的回复具有的平均长度比训练语料小4左右（post在train中出现不同次数同样适用）；
  5. 如果glimpse大小取训练语料中response最大长度的二分之一，与常规训练方式相比，该方法得到的perplexity会小一半左右，同时出现perplexity等于0的情况（response为空）；
  6. 猜想：在post和resp唯一对应的情况下，perplexity适合用来评估对话系统的性能。
