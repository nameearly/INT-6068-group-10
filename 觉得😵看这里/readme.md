          
## 🎯 项目演进逻辑与新手入门指南

作为强化学习新手，我来为你梳理这个项目的完整演进路径和启动顺序：

### 📋 **项目演进时间线**

```
阶段1: 深度学习实验 (基础算法研究)
    ↓
阶段2: PyBullet物理仿真 (单智能体真实环境)  
    ↓
阶段3: 简化多智能体仿真 (多无人机协调)
    ↓
阶段4: 奖励函数优化 (当前状态)
```

### 🚀 **新手启动顺序（推荐）**

#### **第1步：从深度学习实验开始** ⭐ **最适合新手**
**原因**：环境简单，算法清晰，易于理解和调试

```bash
# 进入最简单的实验环境
cd d:\INT-6068-group-10\深度学习尝试\deeplearning1

# 运行基础训练
python train.py
```

**关键参数调优位置**：
- **训练回合数**：`max_episodes = 1000`（[train.py:18](file:////INT-6068-group-10/深度学习尝试/deeplearning1/train.py#L18)）
- **每回合步数**：`for t in range(200)`（[train.py:25](file:////INT-6068-group-10/深度学习尝试/deeplearning1/train.py#L25)）
- **经验池大小**：`ReplayBuffer(capacity=100000)`（[train.py:16](file:////INT-6068-group-10/深度学习尝试/deeplearning1/train.py#L16)）

#### **第2步：进阶到deeplearning2**
**改进**：支持多轮实验和更系统的超参数调优

```bash
cd d:\INT-6068-group-10\深度学习尝试\deeplearning2

# 运行带输出目录的实验
python train.py --output_dir pst/run_001
```

#### **第3步：PyBullet物理仿真**
**进阶**：真实物理环境，更复杂的状态空间

```bash
cd d:\INT-6068-group-10\基于pybullet的仿真模拟训练\pybullet 版 7.21

# 路径规划训练
python train_rl.py --env path --timesteps 100000

# 动力学控制训练  
python train_rl.py --env dynamics --timesteps 100000
```

#### **第4步：多智能体仿真**
**高级**：多无人机协调，最复杂的场景

```bash
cd d:\INT-6068-group-10\简化仿真模拟环境下的结果\静态模拟

# 运行多智能体环境
python 结合体.py
```

### 🔧 **关键调参位置速查表**

| 参数类型 | 文件位置 | 推荐新手值 | 说明 |
|---------|---------|------------|------|
| **学习率** | [td3.py:18-19](file:////INT-6068-group-10/深度学习尝试/deeplearning1/td3.py#L18) | `lr=3e-4` | Adam优化器学习率 |
| **折扣因子** | [td3.py:24](file:////INT-6068-group-10/深度学习尝试/deeplearning1/td3.py#L24) | `discount=0.99` | 未来奖励衰减系数 |
| **噪声参数** | [td3.py:25-26](file:////INT-6068-group-10/深度学习尝试/deeplearning1/td3.py#L25) | `policy_noise=0.2` | 探索噪声强度 |
| **网络更新频率** | [td3.py:28](file:////INT-6068-group-10/深度学习尝试/deeplearning1/td3.py#L28) | `policy_freq=2` | 策略网络更新间隔 |
| **奖励缩放** | [environment.py:54](file:////INT-6068-group-10/深度学习尝试/deeplearning1/environment.py#L54) | `reward = -distance * 0.1` | 距离奖励系数 |
| **碰撞惩罚** | [environment.py:58](file:////INT-6068-group-10/深度学习尝试/deeplearning1/environment.py#L58) | `reward -= 5` | 边界碰撞惩罚 |

### 📊 **训练监控指标**

1. **实时指标**：每回合奖励（控制台输出）
2. **训练日志**：`training_log.csv`（回合奖励、步数）
3. **模型保存**：每100回合保存中间模型（`td3_actor_XXX.pth`）

### 🎯 **新手建议的实验顺序**

```python
# 实验1：基础训练（默认参数）
python train.py

# 实验2：减少训练回合（快速验证）
# 修改 max_episodes = 200
python train.py

# 实验3：调整探索噪声（观察收敛速度）
# 修改 policy_noise = 0.1 或 0.3
python train.py

# 实验4：调整奖励缩放（观察策略变化）
# 修改 reward = -distance * 0.05 或 0.2
python train.py
```

### ⚠️ **注意事项**

1. **从简单开始**：先掌握deeplearning1，再逐步进阶
2. **小步试错**：每次只改一个参数，观察效果
3. **记录实验**：保存不同参数组合的训练结果
4. **监控收敛**：关注奖励曲线的变化趋势

这样的渐进式学习路径能让你逐步理解强化学习的核心概念，同时避免被复杂的环境和算法淹没。
        
