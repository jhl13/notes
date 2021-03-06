## Few-shot Object Detection via Feature Reweighting
阅读笔记 by **luo13**  
2020-3-9  

这篇论文的主要思想要让网络从支持集中学到特征毕竟指导网络从查询集中检测出目标。个人觉得有三个点值得学习。  
1、还是得有一个大的数据集做支撑。  
2、不同于通常的目标检测算法，训练规则得模拟少样本的时候。  
3、如何结合查询集和支持集所提取到的不同特征。  

**网络结构**  
![网络结构](../../../img/reweighting/网络结构.png)   
Feature Extractor负责提取查询集的特征，Reweighting moudle负责提取支持集的特征，支持集应该每一个只包含一类物体（不清楚可不可以包含一类的多个，或者包含重复的类），并用mask标记出gt的位置一起输入到网络中，以便网络能学习到哪些是背景信息。将查询集和支持集结合起来的办法是相关操作。最后输出到预测网络进行预测。  

![相关操作](../../../img/reweighting/相关操作.png)   

**学习策略**  
![任务](../../../img/reweighting/任务.png)   
这样的学习策略可以让网络更好的结合D和R提取出来的特征。作者没有说T有多少个查询集。  

思考：相同的查询集、不同的支持集。或者不同的支持集、相同的查询集。  
