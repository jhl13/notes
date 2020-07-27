## Looking Fast and Slow: Memory-Guided Mobile Video Object Detection
阅读笔记 by **luo13**  
2020-7-13  

文章贡献：  
1、提出了一个交替使用不同模型以提升视频目标检测速度的系统  
2、改进了LSTM，以及更新门使用的频率，使得LSTM性能上升  
3、提出使用强化学习方法自动选择需要较大网络检测的帧  

![LFSM](../../../img/LFSM/概念图.png)   
快慢网络交替使用  

![LFSM](../../../img/LFSM/交替模块.png)   
大致的网络结构，分为特征提取，LSTM，以及检测头，这些东西都是可以更换的  

![LFSM](../../../img/LFSM/改进的LSTM.png)   
改进的点主要有两个：  
1、在LSTM内部使用了组卷积进行加速  
2、加入了backbone，且将这一部分的输出同时concat到输出门的输出，这样LSTM也会有较大的当前帧特征  
3、只有slow network前向时才更新input gate，避免fast network使得LSTM退化  

![LFSM](../../../img/LFSM/训练的策略.png)   
训练分两步  

![LFSM](../../../img/LFSM/异步计算.png)   
**总感觉异步计算会使得关键帧的选择退化，因为更新不是实时的，这时候的效果的确和直接使用异步计算效果差不多**  

![LFSM](../../../img/LFSM/效果和帧率.png)   

![LFSM](../../../img/LFSM/自动选择算法.png)   
使用到了强化学习，没太看懂
