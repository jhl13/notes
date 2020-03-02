## Bayesian Decision Theory
阅读笔记 by **luo13**

### 最小错误率贝叶斯决策
若$P(w_i|x)=\max\limits_{j=1,2}P(w_i|x)$,则$x\in w_i$  
其中  
$$P(w_i|x)=\frac{p(x|w_i)P(w_i)}{p(x)}=\frac{p(x|w_i)P(w_i)}{\sum\limits_{j=1}^{2}p(x|w_j)P(w_j)} \quad i=1,2$$  
$P(w_i)$为先验概率，${p(x|w_i)}$为类条件概率密度，若$x$独立，$x$所取的特征独立，则具体求法可以参考博客[Bayes_Estimation](.\Bayes_Estimation.md)

### 最小风险贝叶斯决策
条件风险通常有一个风险表  
条件风险为$R(\alpha_i|x)=\sum\limits_{j=1}^{c}\lambda(\alpha_i|w_i)P(w_i|x), \quad i=1,...,k$  
在各种决策中选风险最小的决策$\alpha=\argmin\limits_{i=1,...,k}R(\alpha_i|x)$  
$\lambda_{12}=\lambda(\alpha_1,w_2)$代表把属于第二类的样本分到第一类的损失。  
$${\begin{cases}
{\lambda_{11}P(w_1|x)+\lambda_{12}P(w_2|x) < \lambda_{21}P(w_1|x)+\lambda_{22}P(w_2|x),\qquad 则x\in w_1}\\
{\lambda_{11}P(w_1|x)+\lambda_{12}P(w_2|x) > \lambda_{21}P(w_1|x)+\lambda_{22}P(w_2|x),\qquad 则x\in w_2}
\end{cases}}$$
