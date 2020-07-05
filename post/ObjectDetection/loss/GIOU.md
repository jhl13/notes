## Generalized Intersection over Union: A Metric and A Loss for Bounding Box Regression
阅读笔记 by **luo13**  
2020-3-3  

GIOU Loss是IOU Loss的一个改进版本，个人觉得GIOU最大的贡献在于它解决了IOU Loss无法顾及预测框和真实框不重合的情况。而且因为GIOU考虑到了预测框和真实框的最小包围矩形，所以对尺度变化较大的目标会有比较好的效果。  

**算法流程**  
![算法流程](../../../img/GIOU/算法流程.png)   
文中说到IUO loss和GIOU loss对尺度变化都不敏感，可以理解成IOU loss和GIOU loss是一个占比的度量，不会像数值一样变化非常大。  

**GIOU计算**  
![GIOU计算](../../../img/GIOU/GIOU计算.png)   

但当预测框被真实框包围时，GIOU就退化为IOU了，而且这种情况收敛速度会变慢，个人感觉是因为没有一个明确的优化目标。  

但是这个点是很好的，从评测标准出发，而且解决了尺度变化对损失函数的影响。  
