#### note:
&nbsp;&nbsp;&nbsp;&nbsp;paper针对bert指出，在预训练数据足够多、策略设置得好的情况下，模型效果也能极大的提高：
  1. 数据量：BERT-large 13G -> RoBERTa 160G
  2. 策略：
     + 增加预训练步数，batch size尽可能地大（考虑到显存限制，可使用"梯度累积后再更新"的策略）
     + 剔除next sentence prediction任务
     + 尽可能用长文本训练模型（在训练的前90%step，sample中文本长度为512）
     + 动态调整mask策略（不要在每个epoch中对同一个sample进行相同的mask策略）

#### comment：
  1. 论文首先指出BERT训练耗时长，同时初始化参数对模型影响很大，整个文章偏实验性质；
  2. next sentence prediction是否保留还是应该结合下游的场景进行分析。

#### more:
  1. [BERT王者归来！Facebook推出RoBERTa碾压XLNet制霸三大排行榜](http://mini.eastday.com/mobile/190730180533658.html)
  2. [pytorch code](https://github.com/pytorch/fairseq/tree/master/examples/roberta)
