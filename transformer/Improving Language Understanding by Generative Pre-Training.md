#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper提出使用transformer预训练语言模型，再用训练好的参数针对特定任务进行有监督微调，要点记录如下：
  1. 训练时，使用的是“Attention Is All You Need”中decoder：使用当前词来预测下一个词；
  2. 在supervised fine-tuning时，loss不仅包含了specific task损失，还加入了语言模型的损失；
  3. 通过实验发现，9/12任务效果有提升，部分任务效果提升较明显，eg：8.9% on commonsense reasoning (Stories Cloze Test), 5.7% on question answering (RACE)。

#### comment：
&nbsp;&nbsp;&nbsp;&nbsp;在fine-tuning时加入语言模型的loss应该是想尽量保存语言模型的序列结构，在训练过程中逐步降低语言模型损失的权重会不会好点，因为最终我们是想在specific task中提高准确率，同时训练到一定程度后，非语言模型部分的参数也趋于稳定。

#### more:
  1. [Improving Language Understanding with Unsupervised Learning](https://blog.openai.com/language-unsupervised/)
  2. [tensorflow code](https://github.com/openai/finetune-transformer-lm/)

#### highlight:
  1. We’d like to better understand why language model pre-training of transformers is effective. A hypothesis is that the underlying generative model learns to perform many of the tasks we evaluate on in order to improve its language modeling capability and that the more structured attentional memory of the transformer assists in transfer compared to LSTMs.
  2. Overall, the trend suggests that larger datasets benefit from the auxiliary objective but smaller datasets do not.
