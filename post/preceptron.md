## Preceptron Learning Algorithm
阅读笔记 by **luo13**

### 感知机
假设输入空间是$\mathcal{X} \subseteq \R^{n}$，输出空间是${\mathcal{Y}=\{+1,-1\}}$。输入$x \in \mathcal{X}$表示实例的特征空间，$y \in \mathcal{Y}$表示实例类别。由输入空间到输出空间的函数：
${f(x)=sign(w\cdot{x}+b)}$称为感知机。$w\cdot{x}+b=0$是分类超平面。
其中：
$${sign(x)=\begin{cases}
{+1,\qquad x\geq0}\\
{-1,\qquad x\lt0}
\end{cases}}$$

### 感知机的学习策略
若数据集的正样本和负样本可被完整划分到$w\cdot{x}+b=0$分类超平面$S$的两侧，即对所有${y_i=+1}$的样本i，有$w\cdot{x}+b\gt0$；对于所有${y_i=-1}$的样本i，有$w\cdot{x}+b\lt0$，则称数据集线性可分，否则为线性不可分。
&nbsp;
输入空间上$\R^{n}$的一点${x_0}$到超平面$S$的距离为：$\frac{1}{\left \| w \right \|}\left | w\cdot{x_0}+b \right |$
对于误分类的数据$(x_i,y_i)$显然有$-y_i(w\cdot{x}+b)\gt0$
所以误分类点到超平面$S$的距离为$-\frac{1}{\left \| w \right \|}y_i(w\cdot{x}+b)$
${M}$为误分类集合，所有误分类点到超平面$S$的总距离为$-\frac{1}{\left \| w \right \|}\sum\limits_{x_i\in M}^{}y_i(w\cdot{x}+b)$
&nbsp;
忽略$\frac{1}{\left \| w \right \|}$，感知机学习的损失函数定义为
$$L(w, b)=\sum\limits_{x_i\in M}^{}y_i(w\cdot{x}+b)$$
忽略$\frac{1}{\left \| w \right \|}$的原因个人觉得是这个值只是影响损失函数的幅值，但不会影响其趋势。

### 感知机学习算法
