## M2Det: A Single-Shot Object Detector Based on Multi-Level Feature Pyramid Network
阅读笔记 by **luo13**  
2020-3-3  

感觉没啥好说的，新的一阶段目标检测网络，因为觉得FPN结构网络不够特征融合，最后的特征层没有整合到不同尺寸的特征，所以提出了MLFPN进行特征融合，里面使用了多个小沙漏网络并且设计了一个比较好的特征融合模块。总而言之，获得全局多尺度信息很重要，特征的融合部分也很重要。  

**FPN网络**  
![FPN网络](../../../img/M2Det/FPN网络结构.png) 

**本文网络结构**  
![网络结构](../../../img/M2Det/网络结构.png)   

**SFAM特征融合模块**  
![SFAM](../../../img/M2Det/SFAM.png)   
这里有一个细节，使用了类似SE moudle的shortcut来提取全局信息，先降维再升维是为了获取全局的信息并且可以减少计算量。  

**FFM&TUM**  
![FFM_TUM](../../../img/M2Det/FFM_TUM.png)   

小结：其实很多论文都在解决目标检测中的尺度问题。实现细节没有过多的注意，但是现在目标检测使用沙漏网络的还挺多的，有空可以看看沙漏网络和U-Shape网络的区别。  
