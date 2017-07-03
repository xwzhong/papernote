### On Using Very Large Target Vocabulary for Neural Machine Translation

#### note:
&emsp;&emsp;paper是对decoder部分target vocabulary非常大（10w+）的时候建议使用的stragedy。原因：在seq2seq decoder部分，对于每个timestep都需要计算vocabulary size次向量运算（言外之意是需要计算式7），对于vocabulary集合比较大的情况，其运算量和显存（如果使用GPU）会明显增加，因此作者提出了sample softmax技巧，在training过程中，对于decoder的每个timestep中的output部分，只sample指定大小的vocabulary集合替换完整的词集进行计算。

#### comment:
  1. title提到very large target vocabulary，在本文之前的translation实验中，有取3W、8W大小的词集，所以就此猜测，10W+应该算是比较大的词典；
  2. 为什么是target vocabulary，而encoder部分不考虑？此处需要理解encoder部分是没有output layer的；而且，就算是在decoder中的input vocabulary，其亦可包含两套词集，在此用“target”非常精确；
  3. 理解本文的时候需要理解在decoder部分中，train和test/eval是不同的，在train的时候，groundtruth target是已知的，式6只需计算一个分子，但是在test/eval时，target是未知的，有多少个候选word就需要计算多少个分子，然后再进行排序比较；
  4. 很明显，该方法是在计算能力和显存缺乏的情况下提出的。
