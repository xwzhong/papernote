## insurance QA
| Model |  dev  | test1 | test2 | paper | note |
| ------------- |:-------------:| :-----:|:-----:|:-----:|:-----:|
|  QA-CNN   |  0.6160 | 0.6020 |0.5610|  [arxiv](https://arxiv.org/abs/1602.03609v1)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Attentive%20Pooling%20Networks.md)   |
|   QA-CNN+IRGAN  |  - | 0.6444 |0.6111|[arxiv](https://arxiv.org/abs/1705.10513)|[note](https://github.com/xwzhong/papernote/blob/master/chatbot/IRGAN%EF%BC%9AA%20Minimax%20Game%20for%20Unifying%20Generative%20and%20Discriminative%20Information%20Retrieval%20Models.md)|
|  QA-LSTM/CNN with attention   |  0.6720    |   0.6570     |   0.6330    |   [arxiv](https://arxiv.org/abs/1511.04108)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/LSTM-based%20Deep%20Learning%20Models%20For%20Non-factoid%20Answer%20Selection.md)   |
| QA-LSTM with attention(avg) |   0.6840  |    0.6810    |    0.6220   |   [arxiv](https://arxiv.org/abs/1511.04108)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/LSTM-based%20Deep%20Learning%20Models%20For%20Non-factoid%20Answer%20Selection.md)   |
|    AP-CNN    |  0.6880  |    0.6980    |    0.6630   |   [arxiv](https://arxiv.org/abs/1602.03609v1)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Attentive%20Pooling%20Networks.md)   |
|    AP-BiLSTM   |    0.6840   |    0.7170    |    0.6640   |   [arxiv](https://arxiv.org/abs/1602.03609v1)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Attentive%20Pooling%20Networks.md)   |
|    MULT      |     0.7600     |    0.7520      |     0.7340    |    [arxiv](https://arxiv.org/abs/1611.01747)  |    [note](https://github.com/xwzhong/papernote/blob/master/chatbot/A%20Compare-Aggregate%20Model%20for%20Matching%20Text%20Sequences.md)   |
|    SUBMULT+NN      |     0.7700     |    0.7560      |     0.7230    |    [arxiv](https://arxiv.org/abs/1611.01747)  |    [note](https://github.com/xwzhong/papernote/blob/master/chatbot/A%20Compare-Aggregate%20Model%20for%20Matching%20Text%20Sequences.md)   |
|          |          |          |         |    [arxiv]()  |    [note]()   |

## Wiki QA
|  Model |  MAP  |  MRR  | paper | note |
| ------------- |:-------------:| :-----:|:-----:|:-----:|
|   AP-BiLSTM     |    0.6705     |   0.6842    |  [arxiv](https://arxiv.org/abs/1602.03609v1)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Attentive%20Pooling%20Networks.md)   |
|   AP-CNN     |    0.6886     |     0.6957    |  [arxiv](https://arxiv.org/abs/1602.03609v1)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Attentive%20Pooling%20Networks.md)   |
|  SentLevel   |    0.6930  |    0.7090     |    [uchicago](http://ttic.uchicago.edu/~kgimpel/papers/he+etal.emnlp15.pdf)  |   -   |
|  PairwiseRank+WordLevel   |    0.6930  |    0.7100     |    [semanticscholar](https://pdfs.semanticscholar.org/cf8b/bceaca91f791388a64f3f1a0392d64e41f4f.pdf)  |    [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Noise-Contrastive%20Estimation%20for%20Answer%20Selection%20with%20Deep%20Neural%20Networks.md)   |
|  PairwiseRank+SentLevel   |    0.7010  |    0.7180     |    [semanticscholar](https://pdfs.semanticscholar.org/cf8b/bceaca91f791388a64f3f1a0392d64e41f4f.pdf)  |    [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Noise-Contrastive%20Estimation%20for%20Answer%20Selection%20with%20Deep%20Neural%20Networks.md)   |
|  WordLevel   |    0.7090  |    0.7230     |    [aclweb](http://www.aclweb.org/anthology/N16-1108)  |   -   |
| BiMPM  |   0.7180  |  0.7310   |    [arxiv](https://arxiv.org/abs/1702.03814v3)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Bilateral%20Multi-Perspective%20Matching%20for%20Natural%20Language%20Sentences.md)   |
|  SUBMULT+NN   |    0.7332     |   0.7477      |   [arxiv](https://arxiv.org/abs/1611.01747)  |    [note](https://github.com/xwzhong/papernote/blob/master/chatbot/A%20Compare-Aggregate%20Model%20for%20Matching%20Text%20Sequences.md)   |
|  MULT   |    0.7433     |   0.7545      |   [arxiv](https://arxiv.org/abs/1611.01747)  |    [note](https://github.com/xwzhong/papernote/blob/master/chatbot/A%20Compare-Aggregate%20Model%20for%20Matching%20Text%20Sequences.md)   |
|     |         |         |    [arxiv]()  |    [note]()   |

## TREC QA
|  Model  | MAP clean | MRR clean |  MAP raw | MRR raw | paper | note |
| ------------- |:-------------:| :-----:|:-----:|:-----:|:-----:|:-----:|
|  QA-LSTM with attention    |  0.6896     |    0.7849     | - | -   |  [arxiv](https://arxiv.org/abs/1511.04108)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/LSTM-based%20Deep%20Learning%20Models%20For%20Non-factoid%20Answer%20Selection.md)   |
|   AP-BiLSTM   |   0.7132     |     0.8032     | - | -  | [arxiv](https://arxiv.org/abs/1602.03609v1)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Attentive%20Pooling%20Networks.md)   |
|  QA-LSTM/CNN with attention   |  0.7279      |   0.8240     | - | -    |  [arxiv](https://arxiv.org/abs/1511.04108)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/LSTM-based%20Deep%20Learning%20Models%20For%20Non-factoid%20Answer%20Selection.md)   |
|   WordLevel     |   0.7380       |    0.8270     |   0.7550     |    0.8250     |   [aclweb](http://www.aclweb.org/anthology/N16-1108)  |   -   |
|  AP-CNN   |  0.7530     |    0.8511   | - | -   |   [arxiv](https://arxiv.org/abs/1602.03609v1)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Attentive%20Pooling%20Networks.md)   |
|  PairwiseRank+WordLevel   |    0.7620  |    0.8540     |    0.7640  |   0.8270     |    [semanticscholar](https://pdfs.semanticscholar.org/cf8b/bceaca91f791388a64f3f1a0392d64e41f4f.pdf)  |    [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Noise-Contrastive%20Estimation%20for%20Answer%20Selection%20with%20Deep%20Neural%20Networks.md)   |
|   SentLevel     |   0.7770       |    0.8360     |   0.7620     |    0.8300     |   [uchicago](http://ttic.uchicago.edu/~kgimpel/papers/he+etal.emnlp15.pdf)  |   -   |
|  PairwiseRank+SentLevel   |    0.8010  |    0.8770     |    0.7800|   0.8340     |    [semanticscholar](https://pdfs.semanticscholar.org/cf8b/bceaca91f791388a64f3f1a0392d64e41f4f.pdf)  |    [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Noise-Contrastive%20Estimation%20for%20Answer%20Selection%20with%20Deep%20Neural%20Networks.md)   |
| BiMPM  |  0.8020   |  0.8750    | - | -  |   [arxiv](https://arxiv.org/abs/1702.03814v3)  | [note](https://github.com/xwzhong/papernote/blob/master/chatbot/Bilateral%20Multi-Perspective%20Matching%20for%20Natural%20Language%20Sentences.md)   |
|        |          |         |        |         |   [arxiv]()  |    [note]()   |

