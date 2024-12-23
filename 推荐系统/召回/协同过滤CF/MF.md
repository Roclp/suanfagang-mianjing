从协同过滤中衍生出矩阵分解模型(Matrix Factorization, MF)或者叫隐语义模型：

协同过滤算法的特点：

协同过滤算法的特点就是完全没有利用到物品本身或者是用户自身的属性， 仅仅利用了用户与物品的交互信息就可以实现推荐，是一个可解释性很强， 非常直观的模型。
但是也存在一些问题，处理稀疏矩阵的能力比较弱。

在协同过滤共现矩阵的基础上， 使用更稠密的隐向量表示用户和物品。
通过挖掘用户和物品的隐含兴趣和隐含特征， 在一定程度上弥补协同过滤模型处理稀疏矩阵能力不足的问题。


为了使得协同过滤更好处理稀疏矩阵问题， 增强泛化能力。从协同过滤中衍生出矩阵分解模型(Matrix Factorization, MF)或者叫隐语义模型：

在协同过滤共现矩阵的基础上， 使用更稠密的隐向量表示用户和物品。
通过挖掘用户和物品的隐含兴趣和隐含特征， 在一定程度上弥补协同过滤模型处理稀疏矩阵能力不足的问题。

通过分解协同过滤的共现矩阵（评分矩阵）来得到用户和物品的隐向量


矩阵分解模型:

基于评分矩阵，将其分解成Q和P两个矩阵乘积的形式，获取用户兴趣和物品的隐向量表达。
然后，基于两个分解矩阵去预测某个用户对某个物品的评分了。
最后，基于预测评分去进行物品推荐。

常用的矩阵分解方法有特征值分解(EVD)或者奇异值分解(SVD）

奇异值SVD分解：






矩阵分解的优缺点分析

优点：
泛化能力强： 一定程度上解决了稀疏问题
空间复杂度低： 由于用户和物品都用隐向量的形式存放， 少了用户和物品相似度矩阵， 空间复杂度由n^2降低到(n+m)∗f
更好的扩展性和灵活性：矩阵分解的最终产物是用户和物品隐向量， 这个深度学习的embedding思想不谋而合， 因此矩阵分解的结果非常便于与其他特征进行组合和拼接， 并可以与深度学习无缝结合。
缺点：
矩阵分解算法依然是只用到了评分矩阵， 没有考虑到用户特征， 物品特征和上下文特征， 这使得矩阵分解丧失了利用很多有效信息的机会。
同时在缺乏用户历史行为的时候， 无法进行有效的推荐。
为了解决这个问题， 逻辑回归模型及后续的因子分解机模型， 凭借其天然的融合不同特征的能力， 逐渐在推荐系统领域得到了更广泛的应用。