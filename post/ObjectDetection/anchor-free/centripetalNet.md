## CentripetalNet: Pursuing High-quality Keypoint Pairs for Object Detection
阅读笔记 by **luo13**  
2020-4-5  

目前最好的anchor-free目标检测算法，AP 48%，本文贡献：  
1、一种新的聚合关键点的方法  
2、基于corner pooling的注意力机制  

![效果图](../../../img/centripetalNet/效果图.png)   
本文提出的新的聚合关键点的方法，相比于CornerNet和CenterNet能较大减少误聚合的问题。  

![框架](../../../img/centripetalNet/框架.png)   
图中靠下部分是实例分割的分支，这里暂时不考虑，上面分支则是关键点检测分支，绿色部分是关键点检测的分支，红色部分则是cross-star注意力机制，检测出左上和右下的关键点以及关键点相对于中心点的偏移之后，根据偏移聚合左上和右下的关键点。

![偏差](../../../img/centripetalNet/偏差.png)   
（a）中e^cs是关键点检测分支需要预测的中心点偏移，O是误差偏移（如CornerNet中的一样）。（c）中红色区域是聚合区域，如果左上和右下的关键点偏移值落到了红色区域内，则认为他们是同一个检测框的两个关键点。（b）是cross-star的学习目标

![centripetal shift](../../../img/centripetalNet/centripetal_shift.png)   
centripetal shift的计算，加上了log是为了限制输出的大小  

![中心点](../../../img/centripetalNet/中心点计算.png)   
中心偏差区域的计算，u用来控制区域大小  

![得分](../../../img/centripetalNet/得分.png)   
聚合点靠的越近，回归框的得分越高  

![cross-star_df](../../../img/centripetalNet/cross-star_df.png)   
实验过程中作者发现了经过corner pooling之后特征图上会出现一个类似十字星的形状，为了更好得利用这一信息，作者提出了cross-star的注意力机制，个人理解就是实验corner pooling之后的特征图，加上辅助loss，学习目标是上面偏差图的（b）的情况，也就是说让左上角特征图去学习右下部分的内容，让右下角特征图去学习左上部分的内容。  

![guiding_shift](../../../img/centripetalNet/guiding_shift.png)   
学习只在角点部分进行  

小结：  
1、anchor-free现在还是比较多地在特征值点选择和聚合方面进行优化，基本是换一种特征点选择方法或聚合方法就是一篇新论文。  
2、前人的工作中可能存在他们也没想到的一些可以利用的内容。  
