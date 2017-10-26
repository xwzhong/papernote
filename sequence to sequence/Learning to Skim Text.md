### Learning to Skim Text
#### note:
&emsp;&emsp;文章提到，在使用RNN时，需要读入所有的text，但是text中有冗余信息，可以通过skim这部分文本内容来提高decoder时的速度。其中，使用了reinforcement leanring来学习这个skim过程。

#### comment:
1. 作者首先有复现冗余信息这样一个理论，想通过jump这些不必要的信息来提高测试时的效率，考虑到jump步数为离散变量，所以使用了RN的方法来解决这一问题，所以核心是在RL的实际deploy过程；
2. 从模型的角度来思考，其能jump这部分冗余信息，可能是当前已encoded的信息对接下来k步内容已经有了很高的置信度，所以可直接jump这部分信息（这是从测试的时候考虑的）；
3. 模型起到了一定的正则作用；
4. 对于有jump信息的text，使用文章提到的方法能提高测试时执行的速率，但初步预测，训练时间会比不用该方法要长。如果jump信息少，不仅可能因此增加了训练时间，对测试部分的执行效率也不一定提高。（jump信息：对完整的text剔除掉后仍能不影响模型的预测效果，如分类，文本生成等）；
5. paper3.1部分的试验设置得比较巧妙，人能明显地判断出数据有skip信息，从而据此来训练进而判断模型是否能学到这部分信息；
6. 不同的实验组，其embedding是否固定不一致，有何依据？
7. paper3.1部分为什么要curriculum training scheme？training size很大就能不担心overfitting？

#### practice：
1. jump信息多的时候再考虑使用skim技巧。
2. 如何判断jump信息是否多：a.文本长度是否较长；b.重现短语是否较多；c.是否为特定领域文本等。
3. 对于能提高test部分多少准确率可参照paper不同规格的实验。

#### more reading:
<http://www.jiqizhixin.com/article/2720>
