### Topic Aware Neural Response Generation

#### note:
&emsp;&emsp;在生成式对话中，paper引入了对话的topic信息，从而缩小生成对话时可回答界限，引入topic信息大致分为三步：

1. 预先使用LDA训练topic模型，在加入seq2seq模型训练时，针对每组对话的post使用topic模型得到概率最大的主题类，并用该主题类下的词作为特征，考虑了universal word的剔除，每个词的表示，进而得到topic attention；
2. 将topic attention与context attention放在同一层面，计算decoder部分的隐层s，具体employ的过程可看式6计算s部分；
3. 在decoder中output计算时（式6），侧重生成预先使用post得到的主题下的词。

#### comment:
&emsp;&emsp;在不考虑行文的情况下，有两点值得借鉴：
1. paper将对话的topic信息joint到decoder部分的隐层；
2. 在decoder output部分，使用特定的机制偏向了生成的范围。

#### more reading:
&emsp;&emsp;<https://zhuanlan.zhihu.com/p/27218817>
