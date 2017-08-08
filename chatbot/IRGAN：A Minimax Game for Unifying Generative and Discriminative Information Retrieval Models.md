### IRGAN：A Minimax Game for Unifying Generative and Discriminative Information Retrieval Models

#### note:
&emsp;&emsp;文中提出的IRGAN模型给人眼前一亮，其使用GAN较好地整合了“生成”和“判别”这两种经典思想。原文2.1.1部分对其做了通俗易懂的介绍：the generative retrieval model would try to generate (or select) relevant documents that look like the groundtruth relevant documents and therefore could fool the discriminative retrieval model, whereas the discriminative retrieval model would try to draw a clear distinction between the ground-truth relevant documents and the generated ones made by its opponent generative retrieval model。以该方法用于检索式的对话系统为例，IRGAN主要过程如下：

  1. 生成模型的参数更新。用生成模型找出对query最合适的answer（源代码中包括了groundtruth），然后用判别模型计算这些unlabel answer的reward（其代表的正式判别模型的loss），最后再使用这个reward更新生成模型的参数。更新的特点是，unlabel answer离query的groundtruth越近，reward越小，该answer在生成模型的空间变化越小；
  2. 判别模型的参数更新。首先用生成模型找出最适合当前query的unlabel answer，然后使判别模型尽可能地分开groundtruth和这些answer。

#### comment:
  1. IRGAN这种思想，不仅可以运用于文中提到的生成和判别模型中，甚至可以尝试运用到分类中，生成模型选出最模糊的样本令判别模型尽可能地去区分这些样本；
  2. IRGAN的关键之处是“生成”和“判别”模型的交互过程;
    + a. 由生成模型选出最具对抗性的样本；
    + b. 判别模型针对a得到的样本进行训练。
  3. 判别模型的accuracy会不断上升，生成模型的accuracy会不断下降，在第二次训练时，将判别模型的参数更新到生成模型中，不知道训练效果会不会进一步提升；
  4. paper所讲的内容虽然比较绕，但并不会使论文褪色，结合作者给出的代码更容易理解。

#### [code](https://github.com/geek-ai/irgan)

#### more reading:
[阿里SIGIR 2017论文：GAN在信息检索领域的应用](https://www.jiqizhixin.com/articles/44049401-05c0-4b77-884a-74a21695cb27)
