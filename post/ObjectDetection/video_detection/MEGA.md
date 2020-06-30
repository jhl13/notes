## Memory Enhanced Global-Local Aggregation for Video Object Detection
阅读笔记 by **luo13**  
2020-6-26  

文章贡献：  
1、提出了MEGA结构，解决了视频目标检测中ineffective和insufficient问题。  

个人看法：感觉这一文章相当于relation network in video detection在视频目标检测中的扩展。本质内容还是relation network。这一算法好像没有考虑到实时检测的问题，那时候不能获取到之后的帧。  

![MEGA](../../../img/MEGA/概念图.jpg)  
（a）代表全部帧的信息都连接了起来，(b)代表只连接相邻的部分帧，（c）代表连接较远的帧，（d）是本文提出的方法。

![MEGA](../../../img/MEGA/对比.jpg)  
左图是base model  

1、解决ineffective问题, 使用RPN从一些local frames(关键帧的相邻帧)和global frames中(打乱整个视频)生成一些candidate proposals. 然后使用relation network中提出的relation模块将那些global frame中candidate proposals对应的特征给整合到local frame的candidate proposals的特征中. 这个步骤称为global aggregation stage. 这个步骤之后, global信息就被整合到了local frames中. 再然后local frames内部会再过几层relation得到增强的key frame对应的特征. 这个步骤被称为local aggregation stage. 在这两个步骤之后, key frame就得到了global和local两方面的信息. 因此第一个问题就被简单的解决了. 在具体的实现中, local aggregation stage中使用的relation module会使用位置信息, 而global aggregation stage则不使用。值得注意的是global aggregation和local aggregation都是重复多次的。  

2、 解决insufficient问题，如果只有base model, 关键帧能够得到的global和local信息仍然少的可怜, 在图(a)中, global和local信息都只有4帧. 为了解决这个问题, 我们设计了一个简洁高效的模块Long Range Memory(LRM), 极大地增加了关键帧能够看到的范围. 这个模块的设计受到了Transformer-XL的启发. 它的整个操作流程也非常简单, 之前在做完对某一帧的检测之后, 中间计算出来的所有特征都会被丢弃, 在下一帧的检测流程中我们又得全部从头进行计算. 但实际上这些特征也能够提供非常充分的信息, 那么为什么要全部丢弃, 而不是把它们中的一部分存起来呢? 所以就把它们存起来, 并且在下一帧的检测中也使用这些特征。这一思想不知道能不能用作视频检测中的加速。  

整体算法流程，可以看出，其实中心思想还是relation network。relation network是另一篇完整的论文，还没研读过，这里不做介绍了。  
![MEGA](../../../img/MEGA/算法.jpg)  
