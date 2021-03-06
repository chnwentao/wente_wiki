# 背景

wildml 的[Understanding Convolutional Neural Networks for NLP](http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/) 对此有很详细的解释，[这里](https://blog.csdn.net/liuyuemaicha/article/details/53728242)是中文翻译.


## CNN 用于NLP的一些特点


用与文本的CNN与传统用于图像的CNN有以下的不同:

### inputs: 

不同于图像的像素，大部分NLP任务的输入是句子或文档作为一个矩阵。矩阵的每一行表示一个token，一般是一个分词，但也可以是一个字/字母/偏旁，总之每行都是一个向量，代表一个word.
  
现阶段使用的是 pre-train word embedding：
  
### 卷积层
  
在视图中我们的filters会在图像的局部滑动，但在NLP中，我们一般会使用filters在矩阵的整个行上滑动。所以我们filters的宽度通常是和输入矩阵的宽度是一致的(**卷积核的宽度 == embedding的维度**)。

也就是说每次窗口滑动过的位置都是完整的单词，不会将几个单词的一部分“vector”进行卷积，这也保证了word作为语言中最小粒度的合理性。（当然，如果研究的粒度是character-level而不是word-level，需要另外的方式处理）

e.g.  在图像处理中经常看到的卷积核都是正方形的，比如`4*4`，然后在整张image上沿宽和高逐步移动进行卷积操作。但是nlp中输入的“image”是一个词矩阵，比如,n个words，每个word用200维的vector表示的话，这个”image”就是`n*200`的矩阵，卷积核只在高度上滑动，在宽度上和word vector的维度一致（=200），

### max-pooling

max-pooling 后是一个 scalar

由于卷积核和word embedding的宽度一致，一个卷积核对于一个sentence，卷积后得到的结果是一个vector， `shape=（sentence len - filter window + 1, 1）`，那么，在max-pooling后得到的就是一个Scalar。所以，这点也是和图像卷积的不同之处，需要注意一下。

### filter

NLP中会使用多个 window size / region size 的 filter （一般是 2-5 ） ，每个 window size 又有多个卷积核（num filters）。

正是由于max-pooling后只是得到一个scalar，在nlp中，会实施多个filter window size（比如3,4,5个words的宽度分别作为卷积的窗口大小），每个window size又有num filters个（比如64个）卷积核。一个卷积核得到的只是一个scalar太孤单了，智慧的人们就将相同window size卷积出来的num filters个scalar组合在一起，组成这个window size下的feature vector。最后再将所有window size下的feature vector也组合成一个single vector，作为最后一层softmax的输入。

### 总结
用于NLP的CNNs看起来是这样子的:

![](http://7xiuu0.com1.z0.glb.clouddn.com/18-4-10/7965563.jpg)

## CNN的一些Hyperparameters的理解 

### Narrow vs. Wide convolution

两者的不同，我在CNN 有解释，

一般原则是 你的filter比输入的size还大时是必须使用 Wide convolution 的。

### Stride Size
Stride Size  定义了你的filter在每步中滑动多少，Stride size越大，filters的应用次数就会越少，输出的size就会越小。

一般默认为1， 除非你认为你的输出维度过大，但是显而易见这样会丢失信息。

### Pooling Layers

Pooling layers是对输入做二次抽样。在NLP中，我们一般是完整的池化整个输出，对每个filter只产生一个单一的值(scalar) ,而不是类似图像的对每个filter 输出一个更小的矩阵。

### Channels

在图像识别中，你一般会有RGB（红，绿，蓝）三个channels。你可以在不同的channels上应用具有不同或相同权重的卷积.

在 文本中本来是没有 channels 的概念的。不过可以对你的文本进行不同的表达（不同的 embedding/ 分词 / 语言）后嵌入channel.


# 现状

##  Kim Y’s Paper

这个领域的经典论文是 Kim Y的  Convolutional neural networks for sentence classification[^1]


Kim Y的这个模型很简单，但是却有着很好的性能。[Yoon Kim](http://www.people.fas.harvard.edu/~yoonkim/) 在 自己的 github 上实现了一个版本[here](https://github.com/yoonkim/CNN_sentence) 不过是基于 theano。

后续Denny用TensorFlow实现了这个模型的简单版本[blog here](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/) ， [这里是blog的中文翻译](https://www.jianshu.com/p/ed3eac3dcb39)。这是一个详解 不过质量一般 初学可以参考一下 [here](https://blog.csdn.net/accumulate_zhang/article/details/78504637)


Ye Zhang[^2] 等人对这个模型进行了大量的实验，并给出了调参的建议，[paper here ](https://arxiv.org/abs/1510.03820)

[卷积神经网络(CNN)在句子建模上的应用 | Jey Zhang](http://www.jeyzhang.com/cnn-apply-on-modelling-sentence.html)

# 参考

[1] Kim Y. Convolutional neural networks for sentence classification[J]. arXiv preprint arXiv:1408.5882, 2014.

[2] Zhang Y, Wallace B. A sensitivity analysis of (and practitioners' guide to) convolutional neural networks for sentence classification[J]. arXiv preprint arXiv:1510.03820, 2015.



