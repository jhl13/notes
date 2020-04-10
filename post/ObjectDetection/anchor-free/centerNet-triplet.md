## CenterNet: Keypoint Triplets for Object Detection
阅读笔记 by **luo13**  
2020-4-10  

这篇文章是对cornernet的改进，本文贡献：  
1、在cornernet基础上预测中心点，减少误检率  
2、改进了两种pooling方式，可以更好得获得全局信息  

![流程图](../../../img/centernet-triplet/流程图.png)   
算法流程和cornernet很相似，也是预测角点以及角点的embedding，但是增加了中心点的预测，用于后面减少误检率。同时在角点预测的过程加入了cascade pooling，在中心点预测的时候加入了center pooling。  

![pooling](../../../img/centernet-triplet/pooling.png)   
（a）是center pooling，相当于在两个方向进行corner pooling并将其结合起来。水平方向就是左右pooling相链接，感觉这两个pooling应该不是先后循序的，不然后一个pooling就没有用了。（看代码）（b）是corner pooling。（c）是cascade pooling，大概做法是先做一次corner pooling，卷积后再做一次corner pooling，具体做法可能还要参考代码。  

![pooling](../../../img/centernet-triplet/pooling流程.png)  
两种pooling的图示  

![中心区域](../../../img/centernet-triplet/中心区域.png)  
只要中心区域有和角点同类的中心点，则认为是一个合格的检测框。  
通常小物体分割的格数不用太多，大的物体则需要多一些。作者设计了动态的分割方法。  
![中心区域](../../../img/centernet-triplet/中心区域计算.png)  
面积大于250，则n=5。面积小于250，则n=3  
其实也不是很动态。  

![loss](../../../img/centernet-triplet/loss.png)  
loss与cornernet基本一致。  

小结：多复现别人的论文，注重细节，如果自己找不到好的创新点，就先看看别的论文的不足，我感觉这篇论文也就是这样来的。
