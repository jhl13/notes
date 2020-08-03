## Generalized Focal Loss: Learning Qualified and Distributed Bounding Boxes for Dense Object Detection
阅读笔记 by **luo13**  
2020-7-28  

![generalized_focal_loss](../../../img/generalized_focal_loss/qfc.png)  

目标检测中，分类得分和定位质量得分（论文里指的主要是IoU得分和centerness，不知道yolo那种前后景的能不能用）在训练过程中是独立的，但前向过程中又需要结合在一起，这是不合理的。

本文贡献：  
1、将分类得分和定位质量得分结合在一起  
2、采用了更为一般的分布来回归边界

![generalized_focal_loss](../../../img/generalized_focal_loss/GFL.png)  
![generalized_focal_loss](../../../img/generalized_focal_loss/QFLloss.png)  
作者保留了分类的分支，但是相应的label改成了IoU得分（与iou-aware那篇论文的方法一致），因为去除了定位质量分支，所以这里会存在正负样本不平衡的问题，所以loss的形式还是保留了focal loss的形式，其中$\sigma$是预测值，而y是IoU得分（但感觉这样会依赖于回归分支）  

![generalized_focal_loss](../../../img/generalized_focal_loss/不同的分支.png)  
不同的分类分支和定位质量分支组合，这篇论文采用的方法是end-to-end训练的  

![generalized_focal_loss](../../../img/generalized_focal_loss/边界模糊.png)  
在目标检测中，还存在的一类问题是边界模糊的问题，以前有论文使用高斯分布来拟合边界，这篇文论采用了更一般的分布  
![generalized_focal_loss](../../../img/generalized_focal_loss/dfl1.png)  
![generalized_focal_loss](../../../img/generalized_focal_loss/dfl2.png)  
![generalized_focal_loss](../../../img/generalized_focal_loss/dfl3.png)  
![generalized_focal_loss](../../../img/generalized_focal_loss/dfl4.png)  
![generalized_focal_loss](../../../img/generalized_focal_loss/dfl5.png)  
![generalized_focal_loss](../../../img/generalized_focal_loss/回归目标.png)  
常规的目标检测回归边界可以看成是冲击函数，而这篇文章没有具体规定函数类型，只需要概率分布之和为1即可，通过预测不同偏移值的概率，从而得出最后的值（这里的偏移值是设定好的一系列值，感觉这样的设定很依赖数据集），同时，虽然类别边界存在模糊性质，但通常来说，准确的边界就在gt附近，所以loss着重关注了gt附近两个偏移值（不是很明白这里为什么没有提到其他的偏移值）

小结：这篇论文有些内容感觉没说清楚，后续看看代码https://github.com/implus/GFocal
