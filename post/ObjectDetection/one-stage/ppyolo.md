## PP-YOLO: An Effective and Efficient Implementation of Object Detector
阅读笔记 by **luo13**  
2020-9-4  

文章贡献：  
1、tricks大集合  

![ppyolo](../../../img/ppyolo/网络结构.png)  
网络结构总体遵循YOLOv3算法，将backbone替换成了ResNet-vd-50  

主要用到的tricks有：  
1、Larger Batch Size  
2、EMA  
3、DropBlock  
4、IoU Loss  
5、IoU Aware（需要动态label assignment）  
6、Grid Sensitive  
7、Matri NMS  
8、CoordConv  
9、SPP  
10、Better Pretrain Model  

![ppyolo](../../../img/ppyolo/消融实验.png)  

主要实验内容：  
1、EMA  
2、DropBlock  
3、IoU Loss  
4、IoU Aware  
5、Grid Sensitive  
6、Matri NMS  
