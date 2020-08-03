## Mimicking Very Efficient Network for Object Detection
阅读笔记 by **luo13**  
2020-7-29  

这是一篇目标检测知识蒸馏文章  

文章贡献：  
1、尝试将知识蒸馏应用到目标检测网络  
2、使用了featuremap模仿  
3、使用了两步模仿，进一步提升了小网络的效果  

![mimicking](../../img/mimicking/网络结构.png)  
第一步先训练好RPN网络，然后将图片同时送入大网络和小网络，使用训练好的RPN网络在小网络上提取proposal，并在相应的大网络featuremap上提取proposal，使用spp将featuremap缩小，并将小网络通道数经卷积后与大网络一直，计算l2损失，但这样可能会导致损失非常大

![mimicking](../../img/mimicking/loss.png)  
![mimicking](../../img/mimicking/归一化loss.png)  
作者通过使用尺寸归一化，避免了l2损失较大的问题，这里不清楚是尺寸的归一化还是尺寸加通达归一化

第一步训练完之后，第二步有两种方法，第一种是直接finetune，第二种是finetune，且计算类别输出和边界框回归的l2损失（因为网络已经训练得比较好了，所以这个时候直接模仿输出是有效的）

![mimicking](../../img/mimicking/尺度蒸馏.png)  
最后作者还提出了尺度的知识蒸馏，过程和上述过程基本一致  

思考：如何将这一网络结构应用到一阶段的目标检测网络，对背景进行建模是否效果会更好  
