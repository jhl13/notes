## Few-Shot Object Detection with Attention-RPN and Multi-Relation Detector
阅读笔记 by **luo13**  
2020-3-9  

个人感觉这一篇论文是目前看到的最好的一篇论文。  
1、提出了一个少样本检测的数据集，多类别，少图片。  
2、提出了attention rpn，利用支持集的信息更好地提取检测框。  
3、相关连接的头对支持集和查询集RoI信息进行匹配。  
4、少样本的训练策略。  
与reweighting的论文有点相似的。  

**网络结构**  
![网络结构](../../../img/attention_rpn/网络结构.png)   
权值共享的网络得出feature map，将支持集的做全局平均池化然后和查询集的做卷积操作，生成的feature map用来指导rpn，rpn提取信息之后查询集和支持集做相关性操作得出匹配结果。  

![attention](../../../img/attention_rpn/attention.png)   
![相关操作](../../../img/attention_rpn/相关操作.png)   

因为支持集会有多个，所以像图中支持集的模块也有很多个，支持集分支除了共享网络部分，其他部分是没有参数的。相关操作和目标跟踪的相关操作很像。siamese网络很多都有这样的操作  

**训练策略**  
![训练策略](../../../img/attention_rpn/训练策略.png)   
模拟少样本的情况进行训练

**测试方法**  
![测试方法](../../../img/attention_rpn/测试方法.png)   
