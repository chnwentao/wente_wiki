## fitler

### Narrow VS. Wide Convolution

补零(Zero-padding)：这样我们就可以对矩阵的边缘也施加滤波器。补零的好处是让我们可以控制特征映射的尺寸。添加zero-padding也被称为wide convolution(宽卷积)，而不使用zero-padding的将称为narrow convolution(窄卷积)。 

在TensorFlow中的conv2d的padding参数为’SAME’，如果不采取补零而是缩小像素值，padding参数值设置为’VALID’

补零后输出一个同样大小或是更大的矩阵。（可以看下图）

在NLP中，如果滤波器的长度相对于输入向量的长度比较大，要记住使用宽卷积。

![test](http://7xiuu0.com1.z0.glb.clouddn.com/18-4-10/4187490.jpg)"Narrow vs. Wide Convolution. Filter size 5, input size 7. Source: A Convolutional Neural Network for Modelling Sentences (2014)"

上所示，narrow convolution产出的尺寸是`（7-5）+1=3`，而wide convolution产出尺寸是`（7+2*4-5）+1=11`

## Pooling

池化（也叫亚采样或下采样）降低了每个特征映射的维度，但是保留了最重要的信息。空间池化可以有很多种形式：最大(Max)，平均(Average)，求和(Sum)等等。

max-pooling 是最常用的。

先上经典图：

![](http://7xiuu0.com1.z0.glb.clouddn.com/18-4-10/27365549.jpg)

意义

- 使输入表征（特征维度）更小而易操作
- 减少网络中的参数与计算数量，从而遏制过拟合
- 增强网络对输入图像中的小变形、扭曲、平移的鲁棒性（输入里的微小扭曲不会改变池化输出——因为我们在局部邻域已经取了最大值/平均值）。
- 帮助我们获得不因尺寸而改变的等效图片表征。这非常有用，因为这样我们就可以探测到图片里的物体，不论那个物体在哪。



