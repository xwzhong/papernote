### Bilateral Multi-Perspective Matching for Natural Language Sentences

#### note:
&emsp;&emsp;在两个sentence进行match时，paper提出当前sentence每个step emit的vector与另一sentence所有step emit的vector相关，思路步骤大致如下：
  
  1. Given two sentences P and Q, our model first encodes them with a BiLSTM encoder.
  2. Next, we match the two encoded sentences in two directions P against Q and Q against P. In each matching direction, each time step of one sentence is matched against all timesteps of the other sentence from multiple perspectives.
  3. Then, another BiLSTM layer is utilized to aggregate the matching results into a fixed-length matching vector.
  4. Finally, based on the matching vector, a decision is made through a fully connected layer.

#### comment：
  1. 文中提到的Bilateral与3.2部分w的维度l对应，可以理解为：同样的计算方法，由于初始空间位置不同，从而学到不同的特点，eg：对于式子a-b，对a和b输入不同的值能得到不同的结果，但是都是进行减法运算。不过更进一步，作者仍没有很好地解释初始化的l个向量有何更确切的含义。
  2. 模型的关键在于步骤2——如何衡量vector与matrix的关系，文中提出了四种不同的策略，其中max attentive matching的效果最好。
