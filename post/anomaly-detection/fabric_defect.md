## Deformable Patterned Fabric Defect Detection With Fisher Criterion-Based Deep Learning
阅读笔记 by **luo13**  
2020-4-6  

这一篇也是利用autoencoder做缺陷检测的论文，但与defect inspect那篇有所不同的是，这篇论文有一部分是用到了监督学习，但是感觉上整体流程比较复杂。不过文章里面使用监督学习的基于费雪准则的autoencoder值得关注一下，还有一个是文章说到autoencoder隐藏层数目不用太多，不知道是真是假。总体感觉论文还是比较水的，主要是看看思路。  

![网络结构](../../img/FCSDA/网络结构.png)   
文章说SDA（stacked denoising autoencoder）是多个encoder和decode堆叠起来，输入是原始数据加入了噪声，而重构的图片需要和原始数据进行比对得出损失，从而达到消除噪声的效果。  

**费雪准则**  
![loss](../../img/FCSDA/loss.png)   
![loss](../../img/FCSDA/loss_intra.png)   
![loss](../../img/FCSDA/loss_inter.png)   
加入了费雪准则项，是类间距离变大，类内距离变小。  

**流程**  
![流程](../../img/FCSDA/流程图.png)   
![不合理的地方](../../img/FCSDA/不合理的地方.png)
FCSDA1用来做分类，2用来做检测。1是有监督训练，2是无监督训练，只使用无缺陷样本，用来训练一个图像重构AD（总感觉有点多此一举，2能检测出差异，那直接用2不就好了？）   
最后实验中给出的图片是重构图片和原始图片做比较，和流程中的不一样，而且重构图片感觉和无缺陷图片很像，这样的autoencoder感觉不合理，只用无缺陷样本训练的AD应该对缺陷的响应较小才对。

小结：感觉这篇论文有挺多地方不合理
