# AI 驱动的氧化锆离子电导率优化

## 项目概述

本项目利用**物理信息机器学习（Physics-Informed Machine Learning, PIML）**方法，结合 Arrhenius 物理定律与深度学习，实现对氧化锆（ZrO₂）基固体电解质离子电导率的高精度预测、机理解析与新材料逆向设计。

## 文档站说明

- 本站是 GitHub Pages 静态文档站，用于展示数据清洗流程、实验报告、结果图与公式。
- 本站**不执行** Python 训练脚本、MySQL ETL 或分子/DFT 计算任务；这些任务需在本地或服务器环境运行。
- 源码仓库：
  - 数据清洗：<https://github.com/lanhung/material-conductivity-data-clean>
  - 机器学习分析：<https://github.com/lanhung/material-conductivity-data-analysis-ml>

## 研究亮点

| 指标 | 结果 |
|------|------|
| **PIML 模型精度** | RMSE = 0.2532, R² = 0.9353 |
| **AI 发现最优配方** | ZrO₂ + Sc(7.5%) + Mg(3.2%)，预测电导率 0.092 S/cm @800°C |
| **主动学习效率** | 仅 1 轮迭代即发现近最优材料，比随机策略快 15 倍 |
| **计算验证** | PIML 预测排序与分子动力学模拟 100% 一致 |

## 技术路线

本研究构建了一套完整的 **"数据清洗 → 模型训练 → 机理解析 → 逆向设计 → 多尺度验证"** 闭环流程：

1. **[数据清洗](data-cleaning/index.md)**：Python + LLM + SQL 混合管线，将 2010 条原始文献数据标准化为 1351 条高质量样本
2. **[PIML 模型训练](experiments/01-piml-training.md)**：将 Arrhenius 方程嵌入神经网络，实现物理约束下的电导率预测
3. **[机理深度解析](experiments/02-mechanism-analysis.md)**：隐空间可视化、特征重要性分析、跨元素泛化测试
4. **[基准模型对比](experiments/03-baseline-benchmark.md)**：PIML vs DNN vs Random Forest vs XGBoost
5. **[逆向材料设计](experiments/04-inverse-design.md)**：遗传算法驱动的最优共掺杂配方搜索
6. **[主动学习](experiments/05-active-learning.md)**：不确定性量化与 AI 引导的高效材料发现策略
7. **[稳定性筛选](experiments/06-stability-screening.md)**：基于 Shannon 离子半径的热力学稳定性预测
8. **[分子动力学验证](experiments/07-md-validation.md)**：CHGNet 机器学习力场 MD 模拟验证
9. **[DFT 计算验证](experiments/08-dft-verification.md)**：Quantum Espresso 第一性原理计算框架

## 核心模型架构

PIML 模型由两部分组成：

- **数据驱动编码器**：多层感知机从材料特征中提取隐含信息
- **物理约束层**：强制遵循 Arrhenius 方程 $\log_{10}(\sigma) = \log_{10}(A) - \log_{10}(T) - \frac{E_a}{k_B \cdot T \cdot \ln(10)}$

这使得模型在保持高预测精度的同时，输出具有物理意义的活化能（$E_a$）参数。

## 数据集

- **样本量**：1,351 条氧化锆电导率测量记录
- **来源**：文献数据挖掘
- **掺杂元素**：Y、Sc、Yb、Gd、Mg 等
- **温度范围**：600–1000°C
- **电导率范围**：10⁻⁶ ~ 10⁻¹ S/cm
