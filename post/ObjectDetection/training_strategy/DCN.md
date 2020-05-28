## Deformable Convolutional Networks
阅读笔记 by **luo13**  
2020-5-27  

本文贡献：  
1、提出可变卷积  
2、提出可变ROI Pooling以及可变PS ROI Pooling  

![DCN](../../../img/DCN/可变卷积.png)  
![DCN](../../../img/DCN/正常卷积.png)  
![DCN](../../../img/DCN/可变卷积计算.png)  
可变卷积就是在学习了一个offset，offset field通道数是输入通道的两倍，因为有两个方向的偏移，offset field出来的只是一个归一化的offset值，要经过变换之后才能得到offset，通常是一个较小系数乘上特征层尺度，为的是介绍尺度变化带来的影响。  

![DCN](../../../img/DCN/双线性插值1.png)  
![DCN](../../../img/DCN/双线性插值2.png)  
因为偏置之后通常不会落在整数的像素点上，所以采用双线性插值得到最后的响应

![DCN](../../../img/DCN/可变ROIpooling.png)  
![DCN](../../../img/DCN/可变PSroipooling.png)  
ROI的操作其实是和可变卷积一样的，但是这里的offset分支的输入是ROI区域。需要注意的是，这里的偏移是整块bin去偏移。  

![DCN](../../../img/DCN/消融实验.png)  
可变卷积只要加在backbone最后的几层网络上即可。  
