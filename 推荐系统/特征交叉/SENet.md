m个向量的维度可以不同

SENet对离散特征做field-wise加权
Field :
·用户IDEmbedding 是64维向量。
·64个元素算一个field，获得相同的权重。
如果有m个fields，那么权重向量是m维。

m个用户特征得到m*k个向量

平均池化 AvgPool 得到 m*1
全连接层 FC+ReLU 得到 m/r*1 压缩
全连接层 FC+Sigmoid 得到 m*1 恢复

最后
m*k个向量与 m*1向量逐行相乘 做加权

最后得到 m*k个向量