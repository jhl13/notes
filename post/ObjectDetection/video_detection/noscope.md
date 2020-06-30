## NoScope: Optimizing Neural Network Queries over Video at Scale
阅读笔记 by **luo13**  
2020-6-22  

感觉是一篇水分挺大的论文，本来以为是视频目标检测论文，但其实是一篇视频查询论文  

主要任务是给定视频和需要查询的目标，判断视频帧中有没有出现需要查询的目标  

论文主要分三个模块：  
1）Model Specialization  
针对特定场景训练的轻量级CNN模型，层数和Channel都降到最低。  
2）Difference Detection  
差异性检测，用于跳过与前面帧变化不大的帧，速度更快。  
3）Cost-based Model Search  
基于代价的模型选择，确定合适的模型进行检测。  


