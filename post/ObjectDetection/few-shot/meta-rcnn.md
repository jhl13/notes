## Meta R-CNN : Towards General Solver for Instance-level Low-shot Learning
阅读笔记 by **luo13**  
2020-3-12  

meta-rcnn的结构和faster-rcnn或者maskrcnn是一样，唯一不是很确定的是分类模块是不是固定类别的。（我倾向于不是固定的）

**概念**  
![概念图](../../../img/meta-rcnn/概念图.png)   
少样本识别和少样本检测的概念  

**整体框架**  
![整体框架](../../../img/meta-rcnn/整体框架.png)   
主要是PRN分支会产生class-attentives-vectors与rpn网络得到的特征图进行卷积，class-attentives-vectors是由每一类的object-attentives-vectors取平均得到的，object-attentives-vectors则是把backbone输出全局池化后进行sigmoid得到的。训练的时候使用object-attentives-vectors，测试的时候使用class-attentives-vectors。  

![训练](../../../img/meta-rcnn/训练.png)   
训练的时候会把base和novel的类别混合，再抽取小样本集（meta）进行训练，这可能也是导致别人说他需要重新训练的原因，但如果分类是单独对应PRN输入的类别的话，他其实也是可以做新类别的预测的吧？训练的时候对object-attentives-vectors进行了交叉熵，这一个辅助的meta-loss对效果有很大的提升，具体形式在论文里面没有找到，可以到代码里找一找。  

小结：训练策略还是得用小样本的策略，辅助loss可能对结果又很大帮助
