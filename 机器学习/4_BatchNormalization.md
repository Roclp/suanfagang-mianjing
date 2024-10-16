不同层的数据分布会往激活函数的上限或者下限偏移

BN就是为了解决偏移的，解决的方式也很简单，就是让每一层的分布都normalize到标准高斯分布。（BN是根据划分数据的集合去做Normalization，不同的划分方式也就出现了不同的Normalization，如GN，LN，IN）

# BatchNormalization的作用
①加速网络收敛（加速训练），允许更大的学习率

②防止梯度消失，结合激活函数

③防止过拟合，可以不再使用L2正则化和dropout

④减少对模型初始化权重的依赖

⑤可以把训练数据彻底打乱（防止每批训练的时候，某一个样本都经常被挑选到，文献说这个可以提高1%的精度）

# BatchNormalization的原理

$$
Input:B=\{x_{1...m}\}; \gamma, \beta \quad (这两个是可以训练的参数) \\ 
Output : \{y_i = BN_{\gamma, \beta}(x_i)\} \\
\mu_{B} \leftarrow \frac{1}{m}\sum_{i=1}^{m}{x_i} \\
\sigma_B^2 \leftarrow \frac{1}{m}\sum_{i=1}^{m}{(x_i - \mu_B)^2} \\
\tilde{x}_i = \frac{x_i - \mu_B}{\sqrt{\sigma_B^2 + \varepsilon}} \quad （分母加\varepsilon是为了防止方差为0）\\
y_i = \gamma \tilde{x}_i + \beta
$$


# 参考资料

[六问透彻理解BN(Batch Normalization）](https://zhuanlan.zhihu.com/p/93643523)

[神经网络之BN层](https://www.jianshu.com/p/fcc056c1c200)

[BN层pytorch实现](https://blog.csdn.net/qq_36867398/article/details/103309712)

[BatchNorm的个人解读和Pytorch中BN的源码解析](https://blog.csdn.net/qq_34914551/article/details/102736271?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.nonecase)

[对于BN层的理解](https://blog.csdn.net/qq_26598445/article/details/81950116)