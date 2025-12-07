# LLaMA-7B LoRa 微调项目

本仓库包含基于 LLaMA-7B 模型使用 LoRa（Low-Rank Adaptation）技术进行微调的项目代码，适用于特定任务的模型适配与性能优化。

## 项目描述

本项目实现了对 LLaMA-7B 大语言模型的 LoRa 微调流程，包括数据预处理、模型加载、LoRa 配置、训练过程监控及模型评估等模块。通过 LoRa 技术在保持模型性能的同时大幅降低微调过程中的计算资源消耗，适用于在特定领域数据上进行高效模型适配。

## 环境要求

- Python 3.8+
- CUDA 11.7+（推荐 12.0）
- NVIDIA GPU（建议显存 ≥ 16GB，支持 FP16 计算）
- PyTorch 1.13+

## 安装指南

1. 克隆仓库：
   
   git clone https://github.com/jvjvxia/---LLaMA-7B---LoRa-----
   cd ---LLaMA-7B---LoRa-----
  

2. 安装依赖项：
 
   pip install -r requirements.txt
 

3. 确保已正确配置 CUDA 环境和 NVIDIA 驱动，可通过以下命令验证：
  
   nvidia-smi
 

## 运行步骤

1. 准备数据集：将训练数据放入 `data/` 目录，支持常见格式（如 JSON、CSV 等）
2. 配置训练参数：修改 `configs/training_args.json` 中的参数（学习率、训练轮次等）
3. 启动训练： 
   python src/train.py --config configs/training_args.json
  
4. 查看训练日志：训练过程日志会保存至 `logs/` 目录，包含损失变化、评估指标等信息

## 训练结果说明

- 训练状态信息保存在 `trainer_state.json` 中，包含：
  - 最佳模型指标（`best_metric`）：0.8718411326408386
  - 最佳模型 checkpoint 路径：`./lora-llama-med-e1/checkpoint-832`
  - 完整训练日志（`log_history`）：记录各步骤的损失值、学习率、评估指标等
  - 总训练步数：832 步（计划总步数 850 步）
  - 总计算量（`total_flos`）：8.109431025618125e+17 FLOPs

## 目录结构
 
---LLaMA-7B---LoRa-----/
├── src/                # 源代码目录（训练、评估脚本等）
├── configs/            # 配置文件目录
├── data/               # 数据集目录
├── logs/               # 训练日志目录
├── results/            # 评估结果与可视化文件
├── checkpoints/        # 模型 checkpoint 保存目录
├── requirements.txt    # 项目依赖清单
└── README.md           # 项目说明文档
```

## 注意事项

- LLaMA 模型权重需要根据 Meta 官方要求获取，本仓库不包含基础模型权重
- 微调过程中可根据 GPU 显存调整 `per_device_train_batch_size` 等参数
- 不同任务可能需要调整 LoRa 配置（如秩大小、目标模块等）以获得最佳性能