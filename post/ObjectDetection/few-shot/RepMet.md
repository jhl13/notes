## RepMet: Representative-based metric learning for classification and one-shot object detection
阅读笔记 by **luo13**  
2020-3-8

少样本学习中有一个术语是n-shot k-way，指的是提供k个类别，每个类别有n个样本，同时有一个查询集，这个查询集的类别是k个中的一个。我们的目标是利用这n*k个数据训练一个模型正确分类查询集图片。少样本检测检测也存在这样的n-shot k-way的设定，从k样本中选取各自选取出n个样本（n个样本还不确定是指n张包含类别的图片还是n个包含图片的测试框），并且选取一或多张图片作为测试集，测试的时候只计算属于k个类别的图片的TP和NP，然后重复多次计算mAP。也有从测试集所有的类别各选出n张图片，然后对剩下的图片进行测试的情况。（策略其实可以自己定义，但如果要做对比实验还是得跟别人的一样）

**文章贡献**  
1、提出了一个新的度量学习的方法  
2、将上面的度量学习方法整合到目标检测算法中得到少样本目标检测网络  

**DML learning sub-net**  
![网络结构](../../../img/RepMet/网络结构.png)  
fc的权重就当做是每个类别在度量空间中的高斯分布了  

![fc](../../../img/RepMet/fc.png)  
该子网络的学习目标是学习到一个类别的混合高斯模型，即假设每一个类别都是混合高斯模型，包括k个model（peak）  

![loss1](../../../img/RepMet/loss1.png)  
方差在实验过程中设定为0.5  

![loss2](../../../img/RepMet/loss2.png)  
![loss3](../../../img/RepMet/loss3.png)  
背景的概率使用1-类别概率进行估计  

![loss4](../../../img/RepMet/loss4.png)  

**DML**  
文章一开始把上文提到sub-net应用到DML分类学习中，因为不需要考虑背景，所以使用了一个类似softmax的函数对概率进行估计，但是考虑到了所有的model会不会不好  
![loss5](../../../img/RepMet/loss5.png)  
训练的时候fc那里应该是包含了所有的类别，但是训练的时候每次会选取12个类别，每个类别再挑选4个实例，batch size=48

**few-shot detection**  
少样本检测使用的backbone是FPN-DCN，是预训练好的，只是加上了sub-net之后进行了fine-tune，test的时候讲fc换成相应k-way的类别，整个网络进行fine-tune的效果是最好的。  

小结：  
1、分类网络使用了混合高斯模型，一定程度上可以更好地分类  
2、因为聚类结果（fc的部分）是直接学习的，可能会收敛得更快  
3、RPN网络事预训练模型，感觉没有刻意地去让网络学习支持集里出现过的类别
