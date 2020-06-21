## Objects as Points
阅读笔记 by **luo13**  
2020-6-21  

cornernet提出了一个目标检测的新范式，这种方法现在多被称为keypoint-based。这个方法跳出了主流的anchor-based框架，从特征点方面对目标检测进行了尝试，并取得了一阶段检测最优结果。  

![corner](../../../img/cornernet/算法概述.jpg)  
![corner](../../../img/cornernet/网络结构.jpg)  
CornerNet学习的目标由三个部分组成  
1、heatmap，代表了该像素点属于某一类别的概率，通常维度是Class num+1  
2、embedding，是使用自监督方式学习的一个向量，用来判断两个点属于同一个实例的概率  
3、offset，下采样过程中存在取整操作，这里预测偏移值以便可以消除取整带来的影响  

![corner](../../../img/cornernet/embedding.jpg)  
embedding训练使用自监督方式，向量的内容是无关紧要的，只要满足同类的越相近，异类的距离要大于设定值，embedding的loss只作用于正样本  

![corner](../../../img/cornernet/cornerpooling.jpg)  
![corner](../../../img/cornernet/pooling计算方法.jpg)  
作者选择了角点作为特征点，但是角点在图像中通常没有很明显的界限，作者提出了corner pooling解决这一问题，具体来说就是给定一个像素点，往四个方向按顺序求最大值，相当于一个max pooling的操作。  

![corner](../../../img/cornernet/计算高斯分布.jpg)  
![corner](../../../img/cornernet/高斯减少惩罚.jpg)  
考虑到在角点周围进行小范围偏移，其实也能得到一个比较好的结果，论文就采用了高斯分布来对loss进行平滑，越靠近正样本，惩罚越小。  

![corner](../../../img/cornernet/偏移值.jpg)  
为了解决下采样整数操作带来的影响，作者采用了一个偏移回归对输出进行校正。  

下面是效果对比  
![corner](../../../img/cornernet/效果.jpg)  
