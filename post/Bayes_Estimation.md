## Bayesian estimation
阅读笔记 by **luo13**

### 朴素贝叶斯法
朴素贝叶斯法的缘由是因为其假设了用于分类的特征在类确定的条件下是条件独立的，即：
$${\begin{aligned}
P(X=x|Y=c_k)&=P(X^{(1)}=x^{(1)},...,X^{(n)}=x^{(n)}|Y=c_k)\\
&={\prod\limits_{j=1}^{n}P(X^{(j)}=x^{(j)}|Y=c_k)}
\end{aligned}}$$

先验概率分布$P(Y=c_k),\quad k=1,2,...,K$  
条件概率分布$P(X=x|Y=c_k)=P(X^{(1)}=x^{(1)},...,X^{(n)}=x^{(n)}|Y=c_k),\quad k=1,2,...,K$  
**感觉是将$x$当成是离散变量了**
通过先验概率分布和条件概率分布可以学习到联合概率分布$P(X=x,Y=c_k)=P(X=x|Y=c_k)P(Y=c_k)$#TODO  
由贝叶斯定理可得后验概率
$${\begin{aligned}
P(Y=c_k|X=x)&=\frac{P(X=x|Y=c_k)P(Y=c_k)}{\sum_kP(X=x|Y=c_k)P(Y=c_k)}\\
&=\frac{P(Y=c_k)\prod_jP(X^{(j)}=x^{(j)}|Y=c_k)}{\sum_kP(Y=c_k)\prod_jP(X^{(j)}=x^{(j)}|Y=c_k)}
\end{aligned}}$$

所以朴素贝叶斯分类器可以表示为
$$y=f(x)=\argmax\limits_{c_{k}}\frac{P(Y=c_k)\prod_jP(X^{(j)}=x^{(j)}|Y=c_k)}{\sum_kP(Y=c_k)\prod_jP(X^{(j)}=x^{(j)}|Y=c_k)}$$
因为对于所有类别来说分母都是一样的，所以朴素贝叶斯分类器又可以表示为
$$y=f(x)=\argmax\limits_{c_{k}}{P(Y=c_k)\prod_jP(X^{(j)}=x^{(j)}|Y=c_k)}$$

由上面公式可得，朴素贝叶斯法所采用的原理是后验概率最大化准则。
**而最大化后验概率代表了什么呢？**  
&nbsp;  
这里选择0-1损失函数：  
$$L(Y,f(X))=\begin{cases}
{1, \quad Y\not ={f(X)}}\\
{0, \quad Y ={f(X)}}
\end{cases}$$
这时候期望风险函数为：
$${R_{exp}(f)=E[L(Y,f(X))]}$$  
由联合分布可得  
$${R_{exp}(f)=E_x\sum\limits_{k=1}^K[L(c_k,f(X))]P(c_k|X)}$$  
为了使期望风险最小化，只需对$X=x$逐个极小化，由此可得：  
$${\begin{aligned}
f(x)&=\argmin\limits_{y\in \mathcal{Y}}\sum\limits_{k=1}^KL(c_k,y)P(c_k|X=x)\\
&=\argmin\limits_{y\in \mathcal{Y}}\sum\limits_{k=1}^KP(y\not= c_k|X=x)\\
&=\argmin\limits_{y\in \mathcal{Y}}(1-P(y = c_k|X=x))\\
&=\argmax\limits_{y\in \mathcal{Y}}P(y = c_k|X=x)
\end{aligned}}$$  
**由此可见，后验概率最大化的含义是期望风险最小化**

#### 朴素贝叶斯的参数估计

**极大似然估计**  
先验概率$P(Y=c_k)=\frac{\sum\limits_{i=1}^NI(y_i=c_k)}{N},\quad k=1,2,...,K$  
设第j个特征$x^{(j)}$的取值为${\{a_{j1},{a_{j2}},...,{a_{jS_j}}\}}$，则条件概率为
$$P(X^{(j)}={a_{jl}}|Y=c_k)=\frac{\sum\limits_{i=1}^NI(x_{i}^{(j)}=a_{jl}|y_i=c_k)}{\sum\limits_{i=1}^NI(y_i=c_k)} \quad j=1,2,...,n; \quad l=1,2,...,S_j; \quad k=1,2,...,K$$  
$x_{i}^{(j)}$是第i个样本的第j个特征，$a_{jl}$是第j个特征可能取的第$l$个值；$I$是指示函数  
**学习与分类算法**  
1、计算先验概率以及条件概率  
2、根据给定实例$x=(x^{(1)},x^{(2)},...,x^{(n)})^T$计算${P(Y=c_k)\prod_jP(X^{(j)}=x^{(j)}|Y=c_k)} \quad k=1,2,...,K$
3、根据$\argmax\limits_{c_{k}}{P(Y=c_k)\prod_jP(X^{(j)}=x^{(j)}|Y=c_k)}$确定类别

#### 贝叶斯估计
显然，如果样本数量较少，则可能出现某一先验概率或条件概率为0的情况。  
为了解决这一问题，使用朴素贝叶斯法的贝叶斯估计  
此时条件概率为  
$$P_{\lambda}(X^{(j)}={a_{jl}}|Y=c_k)=\frac{\sum\limits_{i=1}^NI(x_{i}^{(j)}=a_{jl}|y_i=c_k)+\lambda}{\sum\limits_{i=1}^NI(y_i=c_k)+S_j\lambda} \quad j=1,2,...,n; \quad l=1,2,...,S_j; \quad k=1,2,...,K$$  
先验概率为  
$$P(Y=c_k)=\frac{\sum\limits_{i=1}^NI(y_i=c_k)+\lambda}{N+K\lambda},\quad k=1,2,...,K$$  
**概率之和还是等于1**，当$\lambda=1$的时候为拉普拉斯平滑
