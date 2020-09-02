## Deep Inside Convolutional Networks: Visualising Image Classification Models and Saliency Maps
阅读笔记 by **luo13**  
2020-9-2  

神经网络可解释性问题  

本文贡献：  
1、提出了类别模式可视化，可视化分类模型感兴趣的区域或物体  
2、提取梯度可视化方法，通过反向传播明确对分类结果影响较大的像素点（可以利用这一规律进行下游任务，如图像分割或定位）

![maps](../../img/Saliency_Maps/类别模式可视化.png)  
类别模式可视化，固定权重，优化输入，使输入能在特定的类中输出最大的得分  

![maps](../../img/Saliency_Maps/使用原始得分.png)  
在这优化过程中，使用的使网络输出的得分而不是softmax归一化之后的得分  

![maps](../../img/Saliency_Maps/梯度可视化.png)  
梯度可视化，输入图片和label，进行反向传播，得到图像上的梯度值，如果使三通道图片则取其最大的值，梯度值代表，要改变输入，梯度代表，像素值改变对得分的影响大小，所以梯度越大的像素值越重要。

