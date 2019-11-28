## YOLOv3:An Incremental Improvement
阅读笔记 by **luo13**

### 网络结构 #TODO

### 模型优点
1. bboxes的预测，只有overlap最高的预测框才计算分类误差，其余的只计算是否有目标的误差
2. 使用N个sigmod分类器代替了一个N路的softmax分类器，实现了多类标的分类
3. 使用了Darknet-53
4. 多尺度的预测（能预测密集目标的原因）

### 模型缺点 #TODO

### 损失函数

### 实验细节 #TODO

### 性能指标

### 疑问
1. 论文说使用了N个sigmod分类器，但是Darknet-53 table中仍写着softmax