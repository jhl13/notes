## Distilling Object Detectors with Fine-grained Feature Imitation
阅读笔记 by **luo13**  
2020-8-3  

本文贡献：  
1、提出了一种适合一阶段和二阶段目标检测的知识蒸馏训练方法  

![fine-grained](../../img/fine-grained/网络结构.png)  
![fine-grained](../../img/fine-grained/训练方式.png)  
对所有的GT，求与其有交集的说有先验框IoU，根据最大IoU确定阈值，滤除IoU较小的先验框，其他先验框组成一个新的mask，使用这个mask去让student model模仿teacher model。模仿时，并不是直接使用student model的特征输出层，而是加入了一个特征自适应层（实验发现，这样会比较好）

![fine-grained](../../img/fine-grained/损失函数.png)  
损失函数采用了归一化，归一化参数为mask中像素为1的像素总数。  
最后与检测loss加权得到最终的loss   

思考：对远离gt的位置模仿，是否也可以提高性能  
