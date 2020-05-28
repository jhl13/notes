## Bag of Freebies for Training Object Detection Neural Networks
阅读笔记 by **luo13**  
2020-5-26  

这篇论文是object detection tricks的论文。主要研究了mixup、学习率策略、label smooth、多尺度训练以及普通数据增强对目标检测的影响。其中也提到了数据增强对一阶段的目标检测很重要。

![bag](../../../img/bag/视觉连贯mixup.png)  
视觉连贯指的是保持尺度  

![bag](../../../img/bag/mixup消融实验.png)  
不同beta分布对mixup的影响  

![bag](../../../img/bag/mixup效果.png)  
mixup可以缓解对抗攻击，且可以模拟遮挡、拥挤的场景。使得模型在这些情况下更加鲁邦。  

![bag](../../../img/bag/余弦下降学习率.png)  
其实两种方法差不多，但是余弦下降更平缓，也避免了学习率跳动带来的扰动。  

![bag](../../../img/bag/消融实验.png)  
对一阶段来说，数据增强非常重要。二阶段没这么重要的原因可能是二阶段提取ROI其实也相当于一次数据增强了。  

![bag](../../../img/bag/labelsmooth.png)  
文章中说到，label smooth是让网络的输出不用太极端，但我觉得输出是没有变的，还是要趋向1，但label smooth显式地让负样本的概率更小
