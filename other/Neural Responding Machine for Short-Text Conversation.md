### Neural Responding Machine for Short-Text Conversation
#### note:
  
1. 提出的“翻译和对话系统差异”观点个人赞同，闲聊对话是一对多的关系（同个post有多种回复），进一步讲是多对多，而不像文本翻译，原文确定了，译文也“基本”确定了;
2. 文中提的一个概念比较好，使用NRM-glo获取整个post的summarization，NRM-loc表证词的语义（当然，根据单向RNN的特点，当前词的语义自然包含了其之前的语义，如果使用bidretional-RNN就能获取当前词结合前后文本的语义）;
3. 个人之见，NRM-loc已经包含了NRM-glc部分信息，这个可以从两者之见的结构可以看出，文中3.3部分也提出到了它们之见的关系，所以在训练过程中对NRM-loc和NRM-glo分开训练，最后fine tuning，感觉有点牵强;
4. 在实际使用这个模型中（NRM-loc和NRM-glo），算法所学到的attention跟回复中的attention并不对应，个人猜测这是结果不理想（通用性回复多，句子短等）的主要原因，也是开放域的对话系统所遇到的共有难题。所谓回复中的attention，首先得有一个回复的具体点，在这点上再用该模型应该就能很好的生成有语义的具体的回复，而现在的模型学到的是由这些点构成的面（seq2seq算法在多对多语料中训练的结果），从而导致了上述不理想的结果。这是模型在多对多数据下的结果;
5. 有个方面不错，先分开训练NRM-glo和NRM-loc，再合并，因为这种分开训练方式能整合多种机制，特别是无监督学习，如果能通过无监督学习学到大量的语义信息，再整合到seq2seq中，效果可能出乎意料，如skip thought来表征句子语义，OpenAI提出使用语言模型发现的sentiment unit（可以用来控制生成文本的情感）等。

#### comment:
  
* 实验设置思考。
    * 测试集数据量少，test post只有110；
    * 在fine tuning所用数据集中，post:response比值约等于1:1，是不是应该和原training data中的比例相近？

#### [data](http://61.93.89.94/Noah_NRM_Data/):

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实验所用的数据为sina微博，数据质量一般，毕竟是微博评论
