### A simple neural network module for relational reasoning 

#### note:
&emsp;&emsp;paper提出的relational network是为了解决目标（object）之间的关系（relation）问题。

1. 应用场景。给定object之间的关系描述，对给出的关系提问进行回答；
2. paper提出的relational network更多的是一种思想，因此可用于多种形式的关系描述，可以为图像，也可以为文本；
3. RN的实现部分不难，相对简洁（见式1），假设有object A、B、C，先对AB、BC、AC的组合关系进行MLP降维，得到向量a、b、c，再对这三个向量每个元素对应位置相加，得到向量z，最后再对z进行MLP降维。

#### comment:
1. 核心部分在于object该如何利用不同形式（图像、不同类型文本）的语料进行转化；
2. fig2中，不是一个kernel代表一个object。因为一个kernel时计算整张图的结果，代表的是整幅图完整的含义，不同kernel对同一块区域构成的vector代表的是这一块区域不同的映射特征；
3. 实验结果非常吸引人，有break through的意味。
