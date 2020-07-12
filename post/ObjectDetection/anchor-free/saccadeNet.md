## SaccadeNet: A Fast and Accurate Object Detector
阅读笔记 by **luo13**  
2020-7-12

CenterNet的改进网络，多了一个角点的预测以及对边界框的二次回归，角点的预测可以使得网络能学习到更多的边界信息。Corner预测模块是有用的，但感觉计算出角点这一步有点多余。  

![saccadeNet](../../../img/saccadeNet/网络结构.png)  
![saccadeNet](../../../img/saccadeNet/生成角点.png)  
![saccadeNet](../../../img/saccadeNet/整合网络.png)  

