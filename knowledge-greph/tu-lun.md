## 图算法常用库


库名称 |	原始开发语言|	可用某语言调用
-- | --|--
BGL| C++| C++/ Python（通过boost-python）
QuickGraph| C#| 支持.NET平台的任何语言(Python程序员可用IronPython)
igraph| C| C/C++/R/Python（理论上至少有50种语言可直接或间接调用C程序）
NetworkX| 	Pytho|n	Python

NetworkX是一个创建和操纵复杂网络，并对复杂网络的结构、功能和动力学进行研究的Python包，它提供了目前应用最广泛的一些复杂网络分析算法，当然也包括基本的经典图论算法。

我个人认为NetworkX比igraph要好用，因为NetworkX的文档更清晰易读，程序结构组织得也很好，我现在主要在用这个包。但NetworkX的执行效率多数情况下会比igraph要低[见Drew Conway所作的对比](http://files.meetup.com/1406240/sna_in_R.pdf)。所以不适合作太大规模的网络分析计算。

此外，NetworkX和Matplotlib结合得很好，可很方便地进行复杂网络可视化。