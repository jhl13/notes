## Prototypical Networks for Few-shot Learning
阅读笔记 by **luo13**  
2020-3-20  

文章采用距离度量的思想，将特征映射到一个原型空间中，根据支持集样本均值均值得出每一类的原型，使用查询集样本特征与相对应的类原型作对比，得出分类结果。

**概念图**  
![概念图](../../img/prototype_network/概念图.png)  
计算出每一类样本在embedding空间均值作为该类的原型，测试样本跟每一类原型进行对比，距离最近的就是根雷结果，距离度量使用欧式距离。作者也是用了余弦距离做实验，发现余弦距离没有欧式距离好，作者分析的原因是，余弦距离不是严格的凸函数，只有bregman散度下的距离函数，其类别embedding的最优值才是均值。   

使用均值代表类别中心，以及类别的分配上，作者考虑了bregman散度。（均方差是bregman散度的一种）  
https://www.zhihu.com/question/22426561/answer/209945856  
https://blog.csdn.net/wangshun_410/article/details/84963242  
有一篇聚类的论文，后面再看看。  

**算法流程**  
![算法](../../img/prototype_network/算法.png)  
训练过程也是采用meta-learning的训练方式，每次都抽取一些类别，并且每一类都抽取少量的样本（文中训练过程中的采用的类别数是20），个人感觉和普通的metric learning的区别是，metric learning可能更加注重个体，prototype network更注重类别中心。  

总结：  
1、如果不使用对照的方法，距离度量是（唯一一个？）解决开集问题的方法  
2、使用均值代表类别中心，选择的度量方式需要考虑bregman散度  
