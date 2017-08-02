### A Compare-Aggregate Model for Matching Text Sequences

#### note:
&emsp;&emsp;该paper更像是一篇实验性论文，在“general”框架下对其中某一块使用不同的方法比较、组合，该框架思路大致如下：

  1. preprocessing。将sentence转化为matrix，paper使用了LSTM，故每个step emit一个vector；
  2. attention。将Q得到的matrix与A每个step得到的vector进行计算，得到A中每个vector对应于Q加权后的vector h，类似于seq2seq中attention的机制；
  3. comparison。对A中每个step的vector与其对应h进行计算，得到vector t；
  4. aggregation。对步骤3得到的vector t序列使用CNN进行整合。

  而paper主要是对步骤3不同的整合方法进行了实验、比较，使用的方法有：
  
  * standard neural network layer（见式3）
  * neural tensor network（见式4）
  * Euclidean distance or cosine similarity（见式5）
  * element-wise subtraction（见式6）
  * element-wise multiplication（见式7）

#### comment：
&emsp;&emsp;通过实验得到（subtraction+multiplication+nn）结果比（Euclidean distance or cosine similarity）效果更好。原因可能在于，前一种方式得到的是高维的matrix，而后一种方式只是二维的向量，表现能力比较弱，高维包含了更细致的信息；

#### highlight:
&emsp;&emsp;We can see that SUB is closely related to Euclidean distance in that Euclidean distance is the sum of all the entries of the vector tj produced by SUB. But by not summing up these entries, SUB preserves some information about the different dimensions of the original two vectors. Similarly, MULT is closely related to cosine similarity but preserves some information about the original two vectors.

#### question:
  1. QA matching的方式用于闲聊真的合适？paper3.4部分可视化结果表明，匹配正确的case中，model更多学到了Q与A相同词之间的关系，而闲聊中，这种相同词的情况比较少。
  2. aggregation用LSTM效果会更好？

#### [code](https://github.com/shuohangwang/SeqMatchSeq)
