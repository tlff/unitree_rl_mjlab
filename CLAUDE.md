## unitree_rl_mjlab 模块（MJLab）

位于 `modules/unitree_rl_mjlab/`。基于 mjlab + MuJoCo 的强化学习训练项目，支持 Unitree Go2、A2、As2、G1、R1、H1_2、H2 机器人。

### 环境配置

使用 conda 环境 `unitree_rl_mjlab`，Python 3.11。

激活方式：
```bash
conda activate unitree_rl_mjlab
```

### 列出可用任务

```bash
conda activate unitree_rl_mjlab
cd modules/unitree_rl_mjlab
python scripts/list_envs.py
```

常用任务 ID：
| 任务 ID | 说明 |
|---------|------|
| `Unitree-Go2-Flat` | Go2 速度跟踪训练 |
| `Unitree-G1-Flat` | G1 速度跟踪训练 |
| `Unitree-G1-23Dof-Flat` | G1 23Dof 速度跟踪训练 |
| `Unitree-H1_2-Flat` | H1_2 速度跟踪训练 |
| `Unitree-A2-Flat` | A2 速度跟踪训练 |
| `Unitree-R1-Flat` | R1 速度跟踪训练 |
| `Unitree-G1-Tracking-No-State-Estimation` | G1 动作模仿训练 |
| `Unitree-G1-23Dof-Tracking-No-State-Estimation` | G1 23Dof 动作模仿训练 |

### 训练

单 GPU 训练：
```bash
conda activate unitree_rl_mjlab
cd modules/unitree_rl_mjlab
python scripts/train.py Unitree-Go2-Flat --env.scene.num-envs=1024
```

多 GPU 训练：
```bash
conda activate unitree_rl_mjlab
cd modules/unitree_rl_mjlab
python scripts/train.py <任务ID> --gpu-ids 0 1 --env.scene.num-envs=4096
```

继续训练（从 checkpoint 恢复）：
```bash
python scripts/train.py <任务ID> --agent.resume=True
```

动作模仿训练需要指定 motion_file：
```bash
python scripts/train.py Unitree-G1-Tracking-No-State-Estimation --motion_file=src/assets/motions/g1/dance1_subject2.npz --env.scene.num-envs=4096
```

训练结果保存位置：`logs/rsl_rl/<experiment_name>/<date_time>/`
