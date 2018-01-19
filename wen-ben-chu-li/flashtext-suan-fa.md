# flashtext 算法

使用场景: 在大规模文本中 **高效地提取和替换关键词。**

项目链接：[https://github.com/vi3k6i5/flashtext](https://github.com/vi3k6i5/flashtext)

介绍：[FlashText：语料库数据快速清理利器 \| 机器之心](https://www.jiqizhixin.com/articles/2017-11-10-4)

特点：

1. 随着关键词数量的增加，Regex 的耗时呈线性增长，而对于 FlashText 来说并没有影响。
2. 当关键词数量&gt;500 的时候，FlashText 的搜索速度开始超过 Regex

使用注意：

1.  默认是不区分大小写的
2. 一个 standardised name 可以对应 多个 unclean name ， 但是 反之不行。
3.  只返回最长匹配结果，不返回子串。 e.g. keyword : A AB  word ABC--- &gt; AB
4. 严重依赖空格 ，对未分词的中文无法使用， e.g. keyword : A  B， 对  word AB 是无输出的/



