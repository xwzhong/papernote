#### note:
　　文章指出，使用biLSTM构建语言模型预测下一个词A时（假定完整句子为sABCDe），其也利用了A本身的信息（原因在backforward过程，s的输出由A的输入得到），针对这点，作者提出下一个词（A）的预测仅与其上下文（sBCDe）相关，并在IMDB情感二分类实验中提升0.5%的准确率。

#### more:
　　[tensorflow code](https://github.com/dongjun-Lee/birnn-language-model-tf)
