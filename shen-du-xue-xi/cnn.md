## fitler

### Narrow VS. Wide Convolution

补零(Zero-padding)：这样我们就可以对矩阵的边缘也施加滤波器。补零的好处是让我们可以控制特征映射的尺寸。添加zero-padding也被称为wide convolution(宽卷积)，而不使用zero-padding的将称为narrow convolution(窄卷积)。 

在TensorFlow中的conv2d的padding参数为’SAME’，如果不采取补零而是缩小像素值，padding参数值设置为’VALID’

补零后输出一个同样大小或是更大的矩阵。（可以看下图）

在NLP中，如果滤波器的长度相对于输入向量的长度比较大，要记住使用宽卷积。

![](http://7xiuu0.com1.z0.glb.clouddn.com/18-4-10/4187490.jpg)"Narrow vs. Wide Convolution. Filter size 5, input size 7. Source: A Convolutional Neural Network for Modelling Sentences (2014)"

