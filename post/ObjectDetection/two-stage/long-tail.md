## Overcoming Classifier Imbalance for Long-tail Object Detection with Balanced Group Softmax
阅读笔记 by **luo13**  
2020-6-27  

文章主要是关注目标检测中的数据长尾问题。  
文章贡献：  
1、分析了目标检测器在长尾数据中不work的原因  
2、提出了一个可解决长尾数据问题的分类模块

https://github.com/FishYuLi/BalancedGroupSoftmax

![long-tail](../../../img/long-tail/长尾数据可视化.png)   
由上图可以看出，随着某个类别实例的减小，对应类别的分类器的归一化权重也在减小，这里不太清楚这个权重是怎么得到的，后面再看看代码。作者根据上图以及实验得出，影响长尾数据检测效果的原因是softmax分类时，数量多的数据会频繁激活对应的神经元，而长尾数据则没有，这会导致其在softmax中被抑制，从而导致其对应的分类器权重较小，输出概率也较少。  

![long-tail](../../../img/long-tail/BAGS.png)   
![long-tail](../../../img/long-tail/分组.png)   
![long-tail](../../../img/long-tail/平衡数据.png)   
为了解决上面提到的问题，作者提出了BAGS，根据训练数据中实例数量进行分组softmax。同时为了能最后结合各组的输出概率，在每一组中加入了others类别，others类别代表没有在该组出现的其他类别（不清楚包不包括背景）。为了平衡数据量，避免others类别远多于其他类别，文章按照每个批次中的前景实例数进行采用，而如果某一个批次中某一组没有实例，则忽略这一组，并且让其他组的others类别不被激活（具体操作得看代码）  

疑惑：  
文章中提到了两个导致长尾数据检测差的原因：1、长尾数据被抑制。2、长尾数据对应神经元激活少。文章好像只解决了第一个问题。  

文章为什么不尝试sigmoid，sigmoid函数好像不会存在被抑制的情况  

文章方法很多地方用到了proposal，这可能也是其选择二阶段方法做实验的原因，但文章方法能否迁移到一阶段的方法中？

背景的实例数是怎样计算得到的？
