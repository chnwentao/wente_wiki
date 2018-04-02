## 名词解释

### CUDA & cuDNN

CUDA是NVIDIA推出的用于自家GPU的并行计算框架，也就是说CUDA只能在NVIDIA的GPU上运行，而且只有当要解决的计算问题是可以大量并行计算的时候才能发挥CUDA的作用。

cuDNN（CUDA Deep Neural Network library）：是NVIDIA打造的针对深度神经网络的加速库，是一个用于深层神经网络的GPU加速库。如果你要用GPU训练模型，cuDNN不是必须的，但是一般会采用这个加速库。

### CUDA 与 OpenCL 区别

[CUDA 与 OpenCL 区别 - CSDN博客](https://blog.csdn.net/babyfacer/article/details/6863572) 作者是Babyfacer，是资深高性能计算达人
