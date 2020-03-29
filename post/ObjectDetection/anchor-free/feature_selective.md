## Feature Selective Anchor-Free Module for Single-Shot Object Detection
阅读笔记 by **luo13**  
2020-3-29  

![效果图](../../../img/feature_selective/效果图.png)   
这篇文章是在Retinanet上改进的，主要是加入了FASF模块，在训练的过程中将每个实例动态分配到不同的特征层，由相应的特征层负责这些实例的学习。  
本文贡献点：  
1、动态为每个特征层分配实例  
2、anchor-free和anchor-based方法的结合  

**网络结构**  
![分配](../../../img/feature_selective/分配.png)   
这是目前大多anchor-based目标检测方法采取的分配实例的方法，在这种方法中，我们采用认为定义的规则，如面积最大或边长符合某种尺度，将不同的实例分配到不同的特征层中，作者认为这种人工定义的分配规则并不是最优的。  

![与anchorb-base结合](../../../img/feature_selective/与anchorb-base结合.png)   
作者提出使用一个新增加的anchor-free分支实现在线特征选择分配。  

![分支结构](../../../img/feature_selective/分支结构.png)   
新增加的anchor-free分支很简单，所以增加的参数量和计算量不算太多。  

![anchor选择](../../../img/feature_selective/anchor选择.png)   
实现在线特征选择，动态分配实例的原理如下，在前向推理之后，计算每个实例在每个anchor-free分支下的损失，选取损失最小的分支作为负责学习该实例的分支。与普通方法不同的地方是，普通方法会在前向之前通过某一人为定义的规则将实例先分配到某个特征层，该特征层会负责该实例的学习。本文方法是，先进行前向推理，然后在每一个特征层分支中都计算该实例的损失，选取损失最小的分支作为负责学习该实例的分支。主要的不同是分配实例的规则和顺序。  

分类损失采用focal loss，回归损失采用IoU loss。  

下图是学习目标  
![学习目标](../../../img/feature_selective/学习目标.png)   

**对比实验**  
![对比实验](../../../img/feature_selective/对比实验.png)   
从对比实验中感觉直接使用anchor-free的方法比不比anchor-based的方法好很多，但是结合起来之后效果提升还是比较明显的  

小结：使用神经网络替代人工设定的规则（推动深度学习发展的一大定理，但要做起来还是很难的）
