## Matching Networks for One Shot Learning
阅读笔记 by **luo13**  
2020-3-27  

（这篇论文只针对one shot的情况）  
最开始知道这篇文章是因为很多少样本学习的论文都有提到这一文章。本文贡献主要有两个。  
1、设计了一个比较与众不同的特征提取器  
2、使用meta learning的方式进行训练（怎么使用就怎么测试）  

**网络结构**  
![网络结构](../../img/matching_network/网络结构图.png)  
这是一个非常具有迷惑性的结构图，咋一看很简单，这不就是提取特征之后进行对比嘛，但是真正难的是g和f两个特征提取器，g使用了BiLSTM，f则是注意力LSTM。g使用BiLSTM的原因是作者认为应该学到每一个样本与支持集内其他样本的关系，f使用注意力LSTM是因为作者认为支持集样本应该能影响查询集图片的特征提取。感觉也是有道理的，但是作者并没有给出naive的特征提取器的实验对比。  

学习到特征之后，采用加权方法预测  
![加权](../../img/matching_network/加权和预测.png)  
![softmax](../../img/matching_network/softmax.png)  
感觉这个加权不是很必要？直接取最大值不就可以了？  

**特征提取器**  
g  
![g](../../img/matching_network/g.png)   
g比较简单，双向LSTM，输入是每个样本经过CNN后得到的特征值，最终的特征值是LSTM双向隐藏层的输出和CNN特征的和。  

f  
![f](../../img/matching_network/f.png)   
这里标红的地方感觉写错了，觉得应该是rk  
6式是对支持集的softmax  
![迭代softmax](../../img/matching_network/迭代softmax.png)  
查询集的特征就是最后一个隐藏输出的特征。  

关于这两个LSTM的输入顺序问题，作者没有提及，但是输入是经过排序的，可以参考论文：Order matters: Sequence to sequence for sets.

因为对LSTM不是很熟悉，找了一些感觉写得不错的博客  
https://blog.csdn.net/shenxiaolu1984/article/details/53129937  
https://www.jianshu.com/p/a87be4be6080  
