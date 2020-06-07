## Towards Accurate One-Stage Object Detection with AP-Loss
阅读笔记 by **luo13**  
2020-6-5  

这篇论文从AP的角度做分类，但是AP计算需要排序，排序后的loss计算是不可导的，作者结合感知机的权重更新方法，先通过错误率驱动的方法得到排序的梯度，再将这一梯度应用到得分上，使用反向传播进行权值更新。  

![AP-loss](../../../img/AP-loss/排序得分.png)   
因为大量负样本的存在，会使负样本loss覆盖正样本loss（focal loss以及GHM所要解决的问题）  

![AP-loss](../../../img/AP-loss/得分排序以及反向传播.png)   
由上图可以卡出，算法一开始使用感知机相似的权值更新方法得出第一步的梯度，之后将梯度应用到得分上，再使用反向传播更新后续参数  

![AP-loss](../../../img/AP-loss/label分配.png)  
作者将label变成onehot的形式（这里其实不是很懂，接触到的大部分label 分配其实都是onehot的）

![AP-loss](../../../img/AP-loss/计算排序得分.png)   
![AP-loss](../../../img/AP-loss/计算label得分.png)   
分数的计算  

![AP-loss](../../../img/AP-loss/loss计算.png)   
![AP-loss](../../../img/AP-loss/loss计算2.png)   
loss的目的是让正样本的排序得分高于全部的负样本。  

![AP-loss](../../../img/AP-loss/error-driven更新.png)   
因为最后排序那一部分是不可导的，所以作者参考了感知机算法，使用了目标差值直接作为最后一部分的梯度。

![AP-loss](../../../img/AP-loss/ap插值.png)   
参考AP计算的方法对最后一部分的梯度（差值）进行插值，会让训练结果更为平滑。  

感觉loss的计算量会比较大，不知道作者在实现过程中有没有进行优化
