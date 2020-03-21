## FoveaBox: Beyond Anchor-based Object Detector
阅读笔记 by **luo13**  
2020-3-21  

FoveaBox并不算是最好的anchor-free的方法，但个人觉得有三个比较好的地方。  
1、gt的正样本部分使用了边界框内部的区域，并且存在一定区间的缓冲边界作为被忽略的地方。  
2、回归目标归一化，这样应该更容易学习。  
3、使用更加密集的anchor boxes与anchor free的方法作对比，体现了anchor free的优越性。  

**网络框架**  
![框架](../../../img/foveanet/框架.png)  
![预测示意图](../../../img/foveanet/预测示意图.png)  
框架与retinanet是一样的，只是最后不使用anchor。输出的channel也是一样的，一个分支用来分类，另一个分支用来回归。（思考，每个点预测不同的类别，但是每个点只回归一个偏差，这样合适吗？）  

**正负样本的设定**  
正负样本设定由阈值来确定，这样做在一定程度上也解决了边界点质量差的问题。  
![正负样本的设定](../../../img/foveanet/正负样本的设定.png)  

除此之外，还将不同大小的gt分配到了不同的fpn层中，但同一个gt可能存在于不同的层，并没有像guided-achoring那样只存在于一层，某一层可能是忽略。在通过最大IoU计算正样本achor的时候，其实感觉上也有做到把不同的gt分配到不同的层中，毕竟面积和fpn相应层是对应的，但可能区分度会不高。    
![层间预测](../../../img/foveanet/层间预测.png)  

**回归目标归一化**  
回归目标归一化使得网络学习更简单。先放缩会原来的大小，再用相应的层去面积的开方去归一化。（文中说会归一化，但感觉不一定在0-1之间）  
![预测目标](../../../img/foveanet/预测目标.png)  

anchor密集程度和点预测的优劣性  
![retinanet的anchor数目](../../../img/foveanet/retinanet的anchor数目.png)  
