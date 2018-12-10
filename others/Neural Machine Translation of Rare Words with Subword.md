#### note:
&nbsp;&nbsp;&nbsp;&nbsp;针对文本翻译中不常用词，作者提出使用BPE（Bite Pair Encoding）方式对词进行切分。
  1. 动机：the translation of some words is transparent in that they are translatable by a competent translator even if they are novel to him or her, based on a translation of known subword units such as morphemes or phonemes；
  2. 学习BPE：从单字符开始，不断向上合并相邻字符对（每次取最大字符对频率进行合并），直到大于某阈值或无字符对（有点类似于构建哈弗曼树——用尽可能少的字符对编码文本）；
  3. 编码BPE：从单字符开始，将相邻最大频率字符对当做一个字符串，若词典中无该字符串则继续合并。

#### comment:
  1. 该方法能较好地解决OOV的情况，特别是针对数据量比较大任务中。同时该策略不单可用于文本翻译中，也可以用于各类任务；
  2. 实验结果中对source和target语料放在一起学习BPE的效果比单独学习更好，因一起学习能保持rare word切分一致性（此处跟语料相关，不能盲目套用）；
  3. 编码操作除了note中提及的部分，还可以考虑最大前向、后向编码，note中编码继承了学习时的特点——生成尽可能少的词，但是并没有考虑使编码时的元字符串尽可能地少，而最大前向、后向则可以；
  4. 该编码方式能做到对数据集所有文本进行编码，同时，在达到最低词汇表大小要求情况下指定词汇表大小。

#### more:
&nbsp;&nbsp;&nbsp;&nbsp;[代码](https://github.com/rsennrich/subword-nmt)，其中核心的代码是[learn_bpe.py](https://github.com/rsennrich/subword-nmt/blob/master/subword_nmt/learn_bpe.py)
