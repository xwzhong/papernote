### Topic Aware Neural Response Generation

#### note:
&emsp;&emsp;在生成式对话中，paper引入了对话的topic信息，从而缩小生成对话时可回答界限，引入topic信息大致分为三步：

+ a. 预先使用LDA训练topic模型，在加入seq2seq模型训练时，针对每组对话的post使用topic模型得到概率最大的主题类，并用该主题类下的词作为特征，同时将通用词进行剔除，每个词仅用对应的向量表示，并引入context最后一步的输出，增加context的语义，进而得到topic attention；
+ b. 将topic attention与context attention放在同一层面，计算decoder部分的隐层s；
+ c. 在decoder中output的词概率分布分两部分，一个是标准的输出分布，从隐层到输出向量，另一个是context attention与隐层输出结合，得到主题词的概率分布，并将这两个分布相加。

#### comment:
&emsp;&emsp;在不考虑行文的情况下，有两点值得借鉴：
1. paper将对话的topic信息joint到decoder部分的隐层；
2. 在decoder output部分，使用特定的机制偏向了生成的范围。

#### more reading:
1. [如何生成主题相关的对话 | 每周一起读 #11](https://zhuanlan.zhihu.com/p/27218817)
2. [从文本生成看Seq2Seq模型](https://zhuanlan.zhihu.com/p/29967933)
