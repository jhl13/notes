## CSPNET: A NEW BACKBONE THAT CAN ENHANCE LEARNING CAPABILITY OF CNN
阅读笔记 by **luo13**  
2020-6-30  

文章贡献：  
1、实验证明，让网络不同的层重复学习相同梯度不利于网络优化  
2、提出了CSP结构，可以增强网络学习能力，并且可以与其他的现有模型结合  
3、基于YOLOv3的FPN结构提出了EFM结构  

![CSPNet](../../img/CSPNet/densenet.png)  
上图是densenet的网路结构

![CSPNet](../../img/CSPNet/网络结构.png)  
右图是CSPDenseNet的结构，首先将输入分成两部分，一半输入到dense block，输出经过transition之后与另一半concat再经过一次transition，输出最后的结果。  

![CSPNet](../../img/CSPNet/denseNet梯度.png)  
如果是采用densenet模块，因为复用输出特征的原因，dense block后续的参数更新会依赖到前面的输入的梯度，这样就会导致不同的层都在重复学习一部分相同的梯度，作者认为这样不利于网络优化。（但感觉这公式有点问题）

![CSPNet](../../img/CSPNet/cspdensenet梯度.png)  
但采用CSP结构之后，可以达到分开两个分支梯度的效果，个人感觉这里有点像大号的shortcut结构。而且还可以减少一半的计算量  

![CSPNet](../../img/CSPNet/四种不同的结构.png)  
transition起到了截断的功能，C图因为直接concat，最后part1也会包含大量part2部分的梯度。D中part1和part2的梯度完全无关了。B图的CSP结构，则是Part1和Part2有关，但又不至于大量包含Part2的梯度  

![CSPNet](../../img/CSPNet/efm.png)  
多尺度特征融合，有点像Bi-fpn，但是作者说使用了Maxout优化，具体实现倒是没说。  
