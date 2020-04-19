## Revisiting the Sibling Head in Object Detector
阅读笔记 by **luo13**  
2020-4-18  

这篇文章关注的问题是目标检测中分类头和回归头所需要特征不一致的问题。这个问题我感觉在很多的论文都是有所体现的，但是很少人会去分析这一问题。  
文章贡献：  
1、使用类似可变卷积的方法直接改变了候选区域的位置，从而能让分类头和回归头关注不一样的区域。  
2、增加了一个约束条件，加大原候选区域和改变后的候选区域的差异  

![结构图](../../../img/revisiting_the_sibling_head/结构图.png)  
在原来的sibling head上再加入了一个TSD结构，TSD结构主要是利用类似可变卷积的方式改变原来的候选框位置再提取特征。而PC模块主要是要加大sibling head和TSD的差异，显性地让网络学习不一样的特征。

![head](../../../img/revisiting_the_sibling_head/head1.png)  
![head](../../../img/revisiting_the_sibling_head/head2.png)  
图一是正常的head，图二是改进之后的head，主要的差别是候选区域的位置  

![regress](../../../img/revisiting_the_sibling_head/fr.png)  
![regress](../../../img/revisiting_the_sibling_head/pr.png)  
回归头通过学习原候选区域的一个偏移值得到新的候选区域

![cls](../../../img/revisiting_the_sibling_head/detac.png)  
![cls](../../../img/revisiting_the_sibling_head/fc.png)  
分类则是学习gird的偏移并进行可变ROI Pooling  

最后作者认为原来sibling head得到的结果应该与TSD得到的结果有所不同，这样组合起来才能得到更好的结果。所以显示增加了约束让其差距变大。  
![cls](../../../img/revisiting_the_sibling_head/cls限制.png)  
![locate](../../../img/revisiting_the_sibling_head/locate限制.png)  
![loss](../../../img/revisiting_the_sibling_head/总的loss.png)  

小结：虽然这个问题大家都能想到，但作者做了可视化结果分析并将可变卷积思想应用到候选区域的思想很新颖。不过不知道效率如何。
