## Learning from Noisy Anchors for One-stage Object Detection
阅读笔记 by **luo13**  
2020-7-2  

本文贡献：  
1、提出了一个新的loss，根据网络的输出重新确定label的置信度  

文章主要思想是利用了神经网络会对不确定的目标输出较低置信度的特性  

![noise-label](../../../img/noise-label/noise-label.png)  
如图所示，IOU阈值大且被分配为正样本的锚点框可能并不适合作为正样本  

![noise-label](../../../img/noise-label/BCE.png)  
![noise-label](../../../img/noise-label/划分正负样本.png)  
通常目标检测器分类使用BCE loss，而划分正负样本使用的是IOU的阈值，这就会导致前面提到的问题  

根据神经网络的特殊，不确定的输出通常会有比较低的阈值，根据这一特性，作者重新分配了正样本的label  

![noise-label](../../../img/noise-label/soft-label.png)  
$\alpha$是控制阈值，loc_a是定位的得分，文章中是refine后的IOU，cls_c是分类得分  

![noise-label](../../../img/noise-label/正负样本的划定.png)  
划定正负样本是根据refine前的IoU阈值确定的  

![noise-label](../../../img/noise-label/reweight.png)  
同时会根据输出的分类和回归得分重新分配权重，因为loc_a和cls_c进行过归一化，这里使用了f函数增大权重差别。  

![noise-label](../../../img/noise-label/loss.png)  
最后的loss使用了r进行权重加权，但是在负样本中还是直接使用了BCE，没有进行加权，会不会导致负样本数量过多？  
