## Incremental Few-Shot Object Detection
阅读笔记 by **luo13**  
2020-3-12  

因为在这之前看了另一篇rpn网络的少样本检测，感觉这篇的idea不算太突出。主要有三点贡献：  
1、采用了Anchor-free的框架  
2、采用了少样本设置来训练网络  
3、采用了类不相关的方法，使得网络在测试新类别的时候不需要重新训练  

**网络框架**  
![网络框架](../../../img/Incremental/网络结构.png)   
f是一个沙漏网络，跟centernet一样，会生成一组与类别无关的Featuremap  
g网络结构与f前半部分一样  
h是一个网络定位模块  

**训练策略**  
分两个部分训练  
阶段1：直接用base class，使用传统方法训练特征提取器，在这过程中也会训练g和h，但不是很确定g是否和f前半部分共享权值，每一个class code都与f进行卷积操作，得到对应class的featuremap  
阶段2：丢弃掉原来第一阶段训练的g和h，用f的前半部分参数初始化g，重新初始化h，采用小样本集合（meta）训练网络  

![测试流程](../../../img/Incremental/测试流程.png)   
![细节](../../../img/Incremental/细节.png)   

思考：效果好像不是很好  
