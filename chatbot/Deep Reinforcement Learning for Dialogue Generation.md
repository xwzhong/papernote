### Deep Reinforcement Learning for Dialogue Generation

#### note:
&emsp;&emsp;paper想通过引入RL机制来解决使用seq2seq做对话系统时遗留的难题，如通用性回复较多。在具体实现中，作者首先使用seq2seq方法pre-train一个base模型，最后使用RL机制，以两个agent互相对话最终得到的reward来调整base model的参数。

#### comment:
1. 使用RL的过程很清晰，定义了RL机制涉及到的action，state，policy，reward，可以当做RL的简单应用学习；
2. 纵观全文，训练结果的好坏取决于reward公式的设计；在paper中，Ease of answer设计有以偏概全的嫌疑（你不能直接说many of these responses are likely to fall into similar regions in the vector space，需要更科学的解释或证明）；
3. 文章使用RL机制时，有种“为了实现对话特点而设计”，从个人角度观点出发，更应该从“对话目的”角度来设计，而且，简单的使用RL机制来实现对话存疑。

#### code:
* [lua](https://github.com/jiweil/Neural-Dialogue-Generation)
* [python](https://github.com/Marsan-Ma/tf_chatbot_seq2seq_antilm)
