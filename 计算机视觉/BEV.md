什么是BEV：
1. BEV（Bird's Eye View）鸟瞰图 俯视图
2. 尺度变化小：正视图中近大远小，俯视图中尺度变化小，尺寸相对一致（图像、特征）
3. 目标间遮挡小：正视图中目标间遮挡大，俯视图中目标间遮挡小

什么是感知：
一种相应模式，比如人脑对外界的响应
多模态视角输入，环境信息输出

Camera：BEVFormer（图像特征Backbone）
Lidar：Point-based（球面空间关键点） Voxel-based（体素空间，划分为块）
Camera+Lidar：BEVFusion

点云：点的集合 稀疏 无序（近多远少） 3D表征信息（有深度信息） 遮挡（点云丢失）


BEV感知算法分类：
BEV Lidar：
1. Pre-BEV Feature Extraction：先提取Lidar特征，再投影到BEV，生成BEV特征 代表性算法：PV-RCNN
2. Post-BEV Feature Extraction：先转换到BEV视角，再提取BEV特征 代表性算法：PointPillar

BEV Camera：
multi-view 2D shared feature Extraction views transformation（2D 3D） detection head
1. Pre-BEV Feature Extraction：先提取Camera特征，再投影到BEV，生成BEV特征 代表性算法：BEVFormer
2. Post-BEV Feature Extraction：先转换到BEV视角，再提取BEV特征 代表性算法：BEVSegmentation

BEV Fusion：点云+图像特征融合
1. Pre-BEV Feature Extraction：先提取Lidar和Camera特征，再投影到BEV，生成BEV特征 代表性算法：BEVFusion


2D到3D是不确定的（不是一一对应，二十一条射线），缺少深度信息，需要深度估计
3D到2D是确定的

2D到3D的转换模块：深度分布
深度\*图像坐标=相机内参*世界坐标

LSS（Lift，Splat and Shoot）提升 视角转换
深度离散化，为每个像素生成所有可能深度的一个序列（模拟射线）表示深度概率，再为每个点生成特征

Pseudo Lidar
连续深度预测，先预测深度图，再根据原始图像和深度图映射至3D坐标，生成伪点云


3D到2D的转换模块：特征查询 3D到2D构建BEV空间特征
Explicit Mapping：显性映射 生成3D参考点，再根据3D参考点查询BEV特征 DETR
Implicit Mapping：隐式映射 网络自适应学习2D到3D的映射关系 PETR

BEV中的注意力机制：
选择重要的信息，忽视不重要的信息
空间注意力之STN
通道注意力之SENet
混合注意力之CBAM：空间+通道

self-attention：序列内部自注意力机制
q：查询向量，计算和其他元素的相关性
k：键值向量，被计算
v：值向量，被查询

ViT：vision Transformer
Swin Transformer：窗口


融合思路：
前融合(数据级融合)指通过空间对齐直接融合不同模态的原始传感器数据
深度融合(特征级融合)指通过级联或者元素相乘在特征空间中融合跨模态数据
后融合(目标级融合)指将各模态模型的预测结果进行融合，做出最终决策。

data-feature-object 不同level非对称 三者两两交叉都可以融合

