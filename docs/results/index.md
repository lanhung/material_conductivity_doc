# 结果总览

## 模型性能对比

| 模型 | RMSE | R² Score | 特点 |
|------|------|----------|------|
| **PIML (本研究)** | **0.2532** | **0.9353** | 物理可解释，输出活化能 $E_a$ |
| Standard DNN | 0.2518 | 0.9360 | 纯数据驱动，黑盒模型 |
| Random Forest | 0.7222 | 0.4740 | 传统集成学习 |
| XGBoost | 0.7179 | 0.4803 | 传统集成学习 |

## AI 发现的最优材料配方

| 参数 | 数值 |
|------|------|
| **材料体系** | ZrO₂ - Sc - Mg 共掺杂 |
| **Sc 掺杂浓度** | 7.50 mol% |
| **Mg 掺杂浓度** | 3.19 mol% |
| **总掺杂量** | 10.68% |
| **预测电导率 @800°C** | 0.092 S/cm |
| **推荐烧结温度** | 1505°C |
| **稳定性评估** | 亚稳态（四方/立方混合相） |

## 关键结果图表

### PIML 模型预测效果

![PIML 预测值 vs 真实值及活化能分布](../assets/images/piml_prediction_and_ea_dist.png)
*PIML 模型在验证集上的预测效果（左）及预测活化能分布（右）。R² = 0.9353，活化能集中在 ~1 eV，符合物理预期。*

### 材料化学隐空间

![t-SNE 隐空间可视化](../assets/images/paper_latent_space.png)
*t-SNE 降维后的材料化学隐空间。不同颜色代表不同主掺杂元素，模型自发学习到了化学聚类趋势。*

### 特征重要性分析

![活化能特征重要性](../assets/images/paper_feature_importance_Ea.png)
*对活化能 $E_a$ 预测的特征置换重要性分析。烧结时间和掺杂数量是最关键的影响因素。*

### 逆向设计优化过程

![遗传算法优化曲线](../assets/images/paper_inverse_design_ga.png)
*遗传算法驱动的三元共掺杂配方优化过程，约 5 代即收敛至最优区域。*

### 晶格应变理论验证

![活化能与掺杂半径关系](../assets/images/paper_strain_theory_verification.png)
*活化能与平均掺杂离子半径的关系，验证了晶格应变理论的物理趋势。*

### 主动学习效率对比

![AI 引导 vs 随机策略](../assets/images/paper_active_learning.png)
*AI 引导策略仅 1 轮即发现近最优材料，随机策略 15 轮仍未达到同等水平。*

### 不确定性量化校准

![UQ 校准结果](../assets/images/paper_uq_calibration.png)
*Monte Carlo Dropout 不确定性估计，大多数真实值落在 95% 置信区间内。*

### 稳定性相图

![相稳定性映射](../assets/images/validation_stability_map.png)
*AI 发现材料（金色五角星）在相稳定性图中的位置，处于亚稳态高导电潜力区域。*

### 分子动力学验证

![PIML vs MD 计算对比](../assets/images/paper_computational_validation.png)
*PIML 预测与 CHGNet 分子动力学模拟的对比，4 个样本排序 100% 一致。*

### DFT 形成能分析

![DFT 形成能](../assets/images/paper_dft_formation_energy.png)
*DFT 形成能对比：AI 推荐材料呈负形成能（稳定），高浓度 Mg 掺杂呈正形成能（不稳定）。*
