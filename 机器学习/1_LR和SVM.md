# LR和SVM的联系
①都是分类算法：可以做二分类，改进可做多分类

②若不考虑核函数，LR和SVM都是线性分类器

③LR和SVM都是有监督学习算法

④LR和SVM都是判别式模型（对于给定输入x，直接预测出x的类别y，基于条件概率，而不是联合概率）

生成式模型：对于给定输入x，预测出x的类别y，基于联合概率
判别式模型：对于给定输入x，预测出x的类别y，基于条件概率

# LR和SVM的区别
①目标函数不同：
LR使用Logistic Loss，SVM使用Hinge Loss

$$
    LR\ Loss:\ L(\omega,b)=\sum_{i=1}^{m}ln(y_{i}p_{1}(x;\beta)+(1-y_{i})p_{0}(x;\beta)) = \sum_{i=1}^{m}(-y_{i}\beta^{T}x_{i}+ln(1+e^{\beta^{T}x_{i}}))
    \\其中，\beta=(\omega;b), p_{1}=p(y=1|x;\beta), p_{0}=p(y=0|x;\beta) \\
    
    \\ SVM\ Loss:\ L(\omega,b,\alpha)=\frac{1}{2}||w||^2+\sum_{i=1}^{m}\alpha_{i}(1-y_{i}(\omega^{T}x_{i}+b))
$$


    LR： 基于概率理论，通过极大似然估计方法估计参数值

    SVM：基于几何间隔最大化原理

> 补充：
> 
> Logistic Loss：			 $L_{log}(z)=log(1+e^{-z})$                   // 用于 LR
> 
> ​					Hinge Loss：		  	 $L_{hinge}(z)=max(0,1-z)$             // SVM
>
> ​					Exponential Loss：	$L_{exp}(z)=e^{-z}$  								 // Adaboost

②SVM通常使用核函数解决非线性分类问题，而LR通常不使用核函数

③SVM的损失函数中自带正则化项($\frac{1}{2}||w||^2$)，而LR需要另外添加。

# LR和SVM什么时候用？

来自Andrew Ng的建议：

①若feature数远大于样本数量，使用LR算法或者Linear SVM

②若feature数较小，样本数量适中，使用kernel SVM

③若feature数较小，样本数很大，增加更多的feature然后使用LR算法或者Linear SVM

# 如何处理多分类？
①SVM
   
   
方式一：组合多个二分类器来实现多分类器（两种方法OvO或OvR）

①OvO（one-versus-one）: 任意两个类别之间设计一个二分类器，N个类别一共$\frac{N(N-1)}{2}$个二分类器

②OvR（one-versus-rest）: 每次将一个类别作为正例，其余的作为反例，共N个分类器。

> 注：OvO和OvR先训练出多个二分类器，在测试时，新样本将同时提交给所有的分类器进行预测，投票产生		最终结果，将被预测的最多的类别作为最终的分类结果

方式二：直接修改目标函数，将多个分类面的参数合并到一个最优化问题中，一次性实现多分类。

②LR：

方式一： OvR：同上，组合多个logistic 二分类器

方式二： 修改目标函数，改进成softmax回归




特点	逻辑回归 (LR)	支持向量机 (SVM)
模型性质	概率模型，输出概率	几何模型，直接输出类别
决策边界	通过概率阈值（0.5）确定线性边界	通过支持向量确定的最大间隔超平面
损失函数	对数损失 (Log-Loss)	合页损失 (Hinge Loss)
正则化	
�
1
L 
1
​
  和 
�
2
L 
2
​
  正则化	惩罚参数 
�
C 控制软间隔
目标函数	最大化对数似然函数	最大化间隔，最小化误差
对异常值敏感性	较敏感	较不敏感（只关注支持向量）
核方法	通常不用核函数	可通过核方法实现非线性边界（如高斯核、RBF 核）
输出形式	概率值（可以解释概率）	类别决策（不输出概率，除非通过概率校准）
适用场景	适合需要概率输出的任务，如广告点击率预测、推荐系统	适合边界清晰、小数据集的任务，如文本分类、图像分类等

# 参考资料

[LR和SVM的相同和不同](https://www.cnblogs.com/bentuwuying/p/6616761.html)

[SVM学习笔记——SVM解决多分类问题的方法](https://blog.csdn.net/mao_hui_fei/article/details/80452424)

[逻辑回归解决多分类和softmax](https://blog.csdn.net/u012879957/article/details/81197903)