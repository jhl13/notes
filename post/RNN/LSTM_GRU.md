## LSTM AND GRU
阅读笔记 by **luo13**  
2020-4-23  

https://blog.csdn.net/juanjuan1314/article/details/52020607  

简单了解了两种比较常用的RNN结构  
![RNN](../../img/LSTM_GRU/lstm.jpg)   
lstm的提出解决了RNN不能有效解决长序列的问题，主要的贡献点在于增加了一个state cell，这个部分不会受到现有状态太多影响，故能将很远的状态传递到现在。为了能更新state cell，分别加入了遗忘门和输入门，对应第一个和第二个sigmoid函数，是否遗忘和是否输入取决于上一阶段的输出和当前阶段的输入。最后通过一个输出门，由state cell和上一阶段输出和当前输入决定当前阶段输出。  

![RNN](../../img/LSTM_GRU/GRU.jpg)   
GRU是LSTM的变体，其比lstm少了一个门控，且将lstm的两个状态合并为一个状态（lstm的输出门和输入门被GRU的更新门代替），减少了参数量。

