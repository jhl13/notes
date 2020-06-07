## Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks
阅读笔记 by **luo13**  
2020-6-6  

这篇文章提出了一个可以使用unpaired数据进行风格迁移的网络（pix2pix需要成对的数据），作者认为使用对抗损失可以让网络捕捉到两个不同数据集中的风格分布，但在实验过程中发现只使用对抗损失很难训练，所以又提出了网络应该具有循环一致性，即进行风格迁移之后的图片还可以还原回来。  

两个比较好的关于GAN的网站  
https://zhuanlan.zhihu.com/p/28342644  
https://zhuanlan.zhihu.com/p/24767059  

![cyclegan](../../img/cyclegan/paired_unpaired.png)   
成对的图片通常很难收集，而且感觉这样收集的样本对多少会存在歧意  

![cyclegan](../../img/cyclegan/对抗损失.png)   
![cyclegan](../../img/cyclegan/循环损失.png)   
![cyclegan](../../img/cyclegan/循环一致.png)   
个人认为对抗损失是用来拟合两个数据集之间的分布情况的，而循环损失是用来减少生成器的映射范围，避免出现模型崩塌的情况。  

![cyclegan](../../img/cyclegan/总的损失.png)   
![cyclegan](../../img/cyclegan/优化目标.png)   
cyclegan总的损失函数以及优化目标。D的目的是使D（y）变大，使D（G（x））变小，这是L会变大（L的范围是负无穷到0），G的目的是使  D（G（x））变大，这时候L变小。  

通常的深度学习算法是梯度下降，由上面的分析可以知道，对抗损失的辨别器是使用梯度上升优化的，而生产器使用梯度下降优化。所以之前看到的论文有说在辨别器前加入梯度反向层，这样可以让生成器提取到那些混淆分别器的，数据集之前共有的特征。    
