## CBAM: Convolutional Block Attention Module
阅读笔记 by **luo13**  
2020-7-1  

本文贡献：  
1、提出了一种新的注意力机制，结合channel层面和spatial层面，对分类和检测都有所提升  

![CBAM](../../img/CBAM/CBAM.png)  
先channel后spatial，这个结果是作者实验得出的，channel解决"what"，即哪个通道需要更加关注，spatial解决"where"，即图像中哪里值得关注  

![CBAM](../../img/CBAM/分模块.png)  
channel attention和spatial attention的实现。channel attention module先通过maxpool和avgpool生成两个C长度的向量，这个向量经过一个共享权重的MLP，结果相加并通过sigmoid函数，最后与原来的特征图相乘。spatial attention module则是通过maxpool和avgpool得到两个H * W的特征图，concat之后经过卷积层得到H*W的特征图最后经过sigmoid之后与原特征图相乘  

![CBAM](../../img/CBAM/resnet-cbam.png)  
cbam是插入到每个conv block中的

文章中的实验部分说明了加入CBAM并不会增加很多参数，但感觉用了全连接应该会增加大量参数才对，特别是在高层channel数特别多的时候  
