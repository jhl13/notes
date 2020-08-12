## Tracking by Instance Detection: A Meta-Learning Approach
阅读笔记 by **luo13**  
2020-8-7  

这篇论文采用小样本的方式，训练一个较好的初始参数，然后使用初始帧fine-tune新的模型。  

本文贡献：  
1、将MAML的方式应用到目标跟踪  
2、提出online-update策略，进一步提升长时间序列跟踪的效果  

![track](../../img/MAML_tracker/域自适应.png)  
思路是将目标检测器迁移到目标跟踪上去  

![track](../../img/MAML_tracker/流程图.png)  
![track](../../img/MAML_tracker/内优化.png)  
![track](../../img/MAML_tracker/外优化.png)  
![track](../../img/MAML_tracker/外优化2.png)  

首先在支持集上通过内优化得到一组参数，使用这些参数在目标集上测试，使用累计误差更新参数。

支持集数据和目标集数据可以是同一序列的，也可以是不同序列的，都是一张图片，支持集图片采用缩放1.08得到三张图，训练阶段使用SD4训练方式，即迭代4次。（不太明白为什么可以不同序列）

![track](../../img/MAML_tracker/参数更新.png)  
参数更新使用可学习的学习率，每个卷积层一个可训练的学习率。  

![track](../../img/MAML_tracker/网络结构.png)  
在训练阶段同时训练offine trainable和online trainable的参数  
在online update过程中只训练online trainable参数  

![track](../../img/MAML_tracker/online-tracking.png)  
online tracking algorithm首先使用初始帧进行SD5学习，然后每一步增加一个最高分的检测框到支持集中，每过一段时间使用更新后的支持集更新参数。  

在线训练的支持集要大于更新间隔，不然loss会为0  

新增的支持集只能算是伪标签，这样真的可以保证参数更新的准确性吗？
