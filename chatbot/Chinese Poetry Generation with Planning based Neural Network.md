### Chinese Poetry Generation with Planning based Neural Network

#### note:
&emsp;&emsp;文章介绍了根据一个句子来生成古诗的模型，流程如下：
![](https://github.com/xwzhong/papernote/blob/master/pic/Chinese_Poetry_Generation_with_Planning_based_Neural_Network_flow.png)

实施步骤如下：
1. 使用textrank提取关键词；
2. 扩展词数（使其与待生成的古诗行数相同）：
    + 方案一：利用训练数据中的古诗，使用textrank抽取一个关键词，每行各有一个，然后利用rnn训练并预测；
    + 方案二：Knowledge-based，利用百科、wordnet进行扩展；
3. 古诗按照如下结构一行一行生成，使用attention引入当前行一定要出现的keyword（生成第二行时，第一行的信息和第二行的keyword作为上下文信息），结构图如下：
![](https://github.com/xwzhong/papernote/blob/master/pic/Chinese_Poetry_Generation_with_Planning_based_Neural_Network_model.png)

#### comment:
1. 文章主要亮点在于生成古诗时，确保了keyword一定会出现在句子中；
2. keyword表示部分建议使用向量进行mask，用于区分上一句古诗（假设不是生成第一句）。


#### more reading:
1. [Chinese Poetry Generation with Planning based Neural Network](https://x-algo.cn/index.php/2018/03/20/chinese-poetry-generation-with-planning-based-neural-network/)
