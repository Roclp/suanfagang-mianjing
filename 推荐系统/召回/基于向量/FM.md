Factorized Machine (FM) 因式分解机

逐渐被淘汰，不常用

线性模型+二阶交叉特征

·FM是线性模型的替代品，能用线性回归、逻辑回归的场景，都可以用FM。
·FM 使用二阶交叉特征，表达能力比线性模型更强。
通过做近似 ui ≈ vi.vj，FM 把二阶交叉权重的数量从 0(d2)降低到 0(kd)