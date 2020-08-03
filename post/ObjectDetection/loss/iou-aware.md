## IoU-aware Single-stage Object Detector for Accurate Localization
阅读笔记 by **luo13**  
2020-7-28  

在one-stage目标检测过程中，会分别预测类别得分和回归边界，这个过程在训练中是相关性较低的，但是在NMS过程中，这两个部分都有很重要的作用，作者认为one-stage定位精度较差的原因就在于分类得分预测和边界回归两个部分相关性低，导致出现了IoU低而分类得分高的情况。作者通过引入IoU得分分支来解决这个问题。（其实这里感觉还是没有将分类得分和边界回归关联起来，因为IoU得分分支也是和分类分支独立的）  

![iou-aware](../../../img/iou-aware/网络结构.png)  
采用retinanet结构，主要是加入了IoU预测的分支，这个分支的gt是预测框与gt的iou得分，是一个动态的值  

![iou-aware](../../../img/iou-aware/iou分支loss.png)  
![iou-aware](../../../img/iou-aware/预测得分.png)  
iou分支采用交叉熵损失，iou分支得分与分类得分相乘得到最后NMS使用的得分  

文章只是显式去预测IoU得分，但感觉IoU分支的好坏取决于回归分支的好坏，而且也没有和分类得分结合起来。
