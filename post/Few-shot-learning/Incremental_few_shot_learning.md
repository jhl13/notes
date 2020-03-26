## Incremental Few-Shot Learning with Attention Attractor Networks
阅读笔记 by **luo13**  
2020-3-26  

Incremental Few-Shot Learning指的是，在学习新类别的同时，网络不会遗忘已经学习到的旧类别信息，novel class指新类别，base class指旧类别。现有的主流的少样本学习方法，如基于度量学习的Siamese网络，或者学习一个良好初始变量的MAML，在学习的过程中会遗忘掉已经学习过的base class，这篇文章主要是提出了一种可以学习novel class以及不会遗忘base class的分类网络。这篇论文是最近放到arxiv上的，感觉还有点东西没写完全，希望后面可以补充完整。Incremental的思想值得借鉴。  

**网络结构**  
![网络结构](../../img/Incremental_few_shot_learning/网络结构.png)   
训练过程分成三个阶段  
第一阶段是预训练阶段，在这个阶段中，有两个目的，一个是学习一个好的基类分类器，即$W_b$，另一个是学习一个好的特征描述，即BackboneCNN的学习，预训练之后在第二阶段的meta-learning固定了backbone的参数(BackboneCNN是否需要固定，作者没有进行讨论)  
第二阶段是meta-learning，主要需要meta参数，这里指的meta参数指的是![meta参数](../../img/Incremental_few_shot_learning/meta参数.png)meta参数的学习是基于最优的$W_b$，所以论文中说到meta参数的学习跟寻常的学习策略有所不同，后面会进行介绍。这一阶段过后会固定meta参数。  
第三阶段是少样本学习阶段，在这阶段只要是基于上两个阶段，学习最优的$W_b$，然后用于测试查询集。从这里可以发现，要想检测新样本还是得重新训练的。这一阶段的训练没有固定backbone。（对这一阶段还是有点疑惑的地方，如果固定了backbone，就没必要学习attention attractor network了，但是不固定backbone，特征提取器得到的特征还适用于基类的分类器吗？）  

总体思想是设计一个简单的$W_b$，并且提前学习一个正则化项，使得在优化$W_b$的同时，不会遗忘原来的基类。

**学习算法**  
![学习算法](../../img/Incremental_few_shot_learning/算法.png)   
meta参数是基于最优的Wb的，所以要先计算出$W_b^*$，后面使用的是RBP，循环梯度下降算法，没有仔细去了解，使用方法可以参考作者给出的代码，这种梯度下降方法可以解决参新需要基于另一个参数最优解的情况。  
https://github.com/renmengye/inc-few-shot-attractor-public  

学习到meta参数之后，会用做第三步的正则化项。  
![正则化](../../img/Incremental_few_shot_learning/正则化.png)   
![uk](../../img/Incremental_few_shot_learning/uk.png)  
![记忆矩阵](../../img/Incremental_few_shot_learning/记忆矩阵.png)   

其实新类和基类经过Attention Attractor Network之后会存在一定的关系，但是很难说是怎样的关系。

Loss使用交叉熵损失，只是同时预测基类和新类  
![support_loss](../../img/Incremental_few_shot_learning/support_loss.png)   
![query_loss](../../img/Incremental_few_shot_learning/query_loss.png)   
![预测](../../img/Incremental_few_shot_learning/预测.png)   

小结：遗忘灾难问题可以通过建立新类和基类的联系来缓解，循环梯度下降方法可以解决参新需要基于另一个参数最优解的情况。  
