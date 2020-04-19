## EfficientDet: Scalable and Efficient Object Detection
阅读笔记 by **luo13**  
2020-4-18  

这篇检测论文达到了目前单模最好效果，文章的三个贡献点：  
1、使用了EfficientNet  
2、使用了混合尺度搜索，得出更好的网络框架  
3、设计了一种轻量型FPN  

第一点在之前的EfficientNet阅读笔记有提及，感觉这个网络的搜索和调参都比较复杂。第二点也是一种模型搜索的方法。这里主要介绍轻量型FPN结构weighted BiFPN。  

![效果](../../../img/efficientdet/效果.jpg)  
这是efficientdet的效果，可以看出效果很好，但是从网上资料来看，要复现结果很难，这可能跟训练环境，预训练模型等因素都有关系。

![网络结构](../../../img/efficientdet/网络结构.jpg)  
网络结构是EfficientNet的backbone+重复的BiFPN，后面的分类头和回归头与RetinaNet一致，都是各个输出尺度上共享权重。  

![bifpn](../../../img/efficientdet/bifpn.jpg)  
bifpn是重PANet改进而来的，去除了PANet单个输出的节点，并且在同一层上实现了跨越连接。同时BiFPN考虑到了每个尺寸需要的特征可能不一样，所以增加了权重机制。  

![融合](../../../img/efficientdet/融合.jpg)  
![融合](../../../img/efficientdet/normalized_fusion.jpg)  
其实我还是觉得作者的实验结果是说得过去的，毕竟不同尺度的特征是包括整个输出的，而不是单独channel或者pixel。  

小结：weighted BiFPN其实是一个带注意力机制的特征融合机制，感觉理论性不足，这种结构性的改进还只是更多地从结果得出结论。  
