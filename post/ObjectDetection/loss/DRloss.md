## DR Loss: Improving Object Detection by Distributional Ranking
阅读笔记 by **luo13**  
2020-7-27  

文章贡献：  
1、将前后景分类转化为排序问题  
2、通过样本概率分布提取正负样本关系的同时减少计算量  

![DRloss](../../../img/DRloss/概率reweight.png)  
虽然文章有重新整合分布的部分，但这里所说的reweight文章中说的不是很清晰。  

![DRloss](../../../img/DRloss/分类得分.png)  
目标检测中前后景loss公式  

![DRloss](../../../img/DRloss/排序.png)  
除了交叉熵损失以外，还能通过排序进行分类（正样本得分高于负样本）  

![DRloss](../../../img/DRloss/排序loss.png)  
遍历所有正负样本进行排序loss计算，计算量大且受样本不平衡问题影响  

![DRloss](../../../img/DRloss/简化排序loss.png)  
简化后的loss计算量减少，但是极值不稳定，且忽略了样本不平衡的问题  

![DRloss](../../../img/DRloss/结合分布.png)  
![DRloss](../../../img/DRloss/结合分布loss.png)  
结合分布之后，可以考虑到全部样本，且计算量也没有原始的排序loss大。权值之和等于1，分布有多种选择，可以是均匀分布，也可以是根据困难样本挖掘之后的分布。论文里使用的是均匀分布。   

但如果直接使用，可能会使网络退化成简化的loss，也就是从均匀分布退化回了冲击函数分布  

![DRloss](../../../img/DRloss/增加约束.png)  
![DRloss](../../../img/DRloss/约束求解.png)  
加入KL散度，约束优化后的分布  
求解使用KTT，没去推导  

![DRloss](../../../img/DRloss/最后loss.png)  
![DRloss](../../../img/DRloss/选择阈值.png)  
作者选择使用logistics函数作为损失函数，主要是考虑到了转折点的平滑性，阈值选择依照训练时的正负排序间隔设置
