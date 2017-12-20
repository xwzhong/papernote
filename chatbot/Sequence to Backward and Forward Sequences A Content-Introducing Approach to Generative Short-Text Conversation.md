### Sequence to Backward and Forward Sequences A Content-Introducing Approach to Generative Short-Text Conversation 

#### note:
&emsp;&emsp;paper依旧是想就生成式对话中解决通用性回复的问题，思路比较简单，在decoder时，预选确定一个有意义的“词”，在一定出现该词的情况下进行扩充从而得到完整的回复，关键部分如下：

1. train：对于一个完整的post-resp对，将“resp”随机选取一个word分割，前后部分设为head和tail，对head部分reverse，得到post-rehead，post-tail对，用两个不同的seq2seq模型进行训练；
2. test/eval：使用petrain得到的PMI信息，计算出当前post出现情况下，最“适合”出现的word（“词”级别），再依次使用反向和正向seq2seq模型得到完整的回复；

#### comment:
1. paper提出的idea降低通用性回复，主要因为预先使用PMI挑出了相对“有意义”的词；
2. 如果只是想进行实验，复现模型相对简单，可以直接套用seq2seq的translate代码，再额外写一个PMI相关计算；
3. 就此模型而言，效果的好坏主要应该在于keywords词表以及test/eval部分keyword的选取；
4. 在train部分，不知道在选取word进行split部分，使用test/eval一样的选取方式效果会不会更好？
  
#### more reading:
1. [教 Chatbot 生成更有营养的对话](https://zhuanlan.zhihu.com/p/27275391)
2. [论文引介 | Sequence to Backward and Forward Sequences](http://chuansong.me/n/1613737151949)
