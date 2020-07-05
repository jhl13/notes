## Region Proposal by Guided Anchoring
阅读笔记 by **luo13**  
2020-3-15  

本文贡献：  
1、不再提前设定anchor大小，而是动态设置每个位置的anchor大小  
2、采用逐像素的概率预测先把大部分anchor中心抑制，减小计算量  


![网络结构](../../../img/guided_anchor/网络结构.png)  
一个FPN的结构，通过guided anchoring模块生成anchor，再在进行过偏移的featuremap上做回归分类。

![totalloss](../../../img/guided_anchor/totalloss.png)  
损失函数是定位loss（每个点是物体的概率值），形状的loss，分类loss以及回归loss  

![不同](../../../img/guided_anchor/不同scale.png)  
绿色是需要预测的中心点位置，黄色是忽略的部分，灰色是负样本区域，要预测的是绿色的部分，根据一定的规则划分这三个区域，并且把相关的区域分配到不同scale的featuremap上，规则是提前设定好的没有详细看论文的设定。如果有重叠的情况，则是高优先级的可以抑制低优先级的   

![最优hw](../../../img/guided_anchor/最优hw.png)  
对hw进行回归存在一个问题，hw的值选什么好呢？根据IoU最大的原则可以确定wh，但是因为hw是一个连续值，如果每个点都要计算与相邻gt的IoU最大的wh，计算量会非常大。作者采用了折中的办法，使用9个设定好的anchor与gt计算IoU，把IoU最大的设定作为该点预测的目标值。  

![shape预测](../../../img/guided_anchor/shape预测.png)  
直接预测anchor的长宽会导致模型不稳定，作者采用了一个类似归一化的操作

![shapeloss](../../../img/guided_anchor/shapeloss.png)  

除此之外，作者说因为guided anchoring生成的proposal质量本来就很大，所以训练的时候可以提到判断正样本的阈值。  
