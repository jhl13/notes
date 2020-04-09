## DenseBox: Unifying Landmark Localization with End to End Object Detection
阅读笔记 by **luo13**  
2020-4-9  

Densebox的工作早在2015年已经完成并且发表，早于Faster-RCNN和FPN，网上不少人说，这篇文章很多超前的思路。但直到2019年，这篇文章的才开始受到更多的关注。文章贡献：  
1、使用类似特征金字塔结构进行特征提取  
2、使用关键点检测目标，使用回归预测边界（FOCS的思想也是一样），没有使用anchor设置  
3、在人脸检测方面增加landmark预测，增加人脸检测精度  

![流程图](../../../img/densebox/流程图.png)   
Densebox首先使用类似于特征金字塔的结构进行特征提取，并使用upsampling增大输出特征图的面积，以便更好检测小目标。利用中心点预测和边界回归的信息得出预测框，进行NMS得出最后的边界框输出。  

![网络结构](../../../img/densebox/网络结构.png)   
使用了VGG19，但是只加载了VGG19前12层的参数，后面参数重新初始化。   

![refine](../../../img/densebox/refine.png)   
refine结构是结合了人脸特征点预测，对人脸中心点进行进一步的优化，这一部分的loss跟人脸中心点分类loss是一样的。  

![total_loss](../../../img/densebox/total_loss.png)   
每部分的loss都是使用l2回归。以gt为中心点，一定半径内的像素点都是正样本，离正样本有一定距离的像素点都是ignore的样本，不计算loss，负样本是采用1%的loss为阈值从全部的负样本中得到的样本。划定的半径距离论文中有定义，但这个可以根据实际需求进行修改。回归loss则是通过一个固定值对回归的长宽进行了归一化，这一固定值可以统计训练集中人脸长宽得到。  

