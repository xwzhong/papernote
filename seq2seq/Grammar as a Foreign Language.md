### Grammar as a Foreign Language 

#### note:
&emsp;&emsp;paper使用了seq2seq+attention机制运用于句子的语法解析上，新瓶装旧酒，模型几乎没变（详细模型参见[bahdanau](https://arxiv.org/abs/1409.0473)论文），只是实验了运用于语法解析上的效果。

#### comment:
1. 语法解析本身的意义有多大？因为DL运用于相关的领域不需要事先具备“语法”知识，当然对于特殊项目的需求除外；
2. 实验设置中讨论了多个因素对结果的影响，这方面值得一看，如：beam size大小的设置及其影响、dropout和pretrain word2vec等；
3. 了解beam size对模型的影响需要理解在training decoder部分，每个timestep都是最大化目标idx，再结合test/eval过程中，beam搜索过程，每个timestep对每个beam进行k次扩展，最后取k个结果作为next timestep的搜索种子。
