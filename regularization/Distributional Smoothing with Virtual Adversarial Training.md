### Distributional Smoothing with Virtual Adversarial Training

#### note:
&emsp;&emsp;文章提出了增加数据smothness（平滑度）的方法：

  1. 动机。input越光滑，其数据本身越整洁（相比于圆形），因此，需要减小其“粗糙”部分（相比于三角形）；
  2. smothness定义。使用[KL divergence衡量](https://github.com/xwzhong/articlelist#math)数据的平滑度。最终得到新的loss方程，见式4.

#### comment:
  1. smothness定义翻译过来，即：输入样本A，随机偏移得到样本B，然后使用KL计算偏移后的分布与原分布的差异（度量光滑度），再尽可能得保证AB被分到同一类中。
  2. vat有三个参数，偏移最大范围ϵ、与原loss方程比例λ和随机次数I；
  3. 无需label标注信息即可用来生成对抗样本；
  4. 实验结果好。
