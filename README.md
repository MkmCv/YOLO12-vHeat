# YOLO-vHeat

[![License: AGPL-3.0](https://img.shields.io/badge/License-AGPL--3.0-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.8--3.12-3776AB.svg?logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.1-EE4C2C.svg?logo=pytorch&logoColor=white)](https://pytorch.org/)

YOLOv12 集成 **vHeat**（基于热传导算子的视觉骨干）的目标检测框架，用于课堂教学行为识别。本项目在 [ultralytics](https://github.com/ultralytics/ultralytics) 基础上二次开发，将 vHeat 模块（如 `C2fHeat`）集成进 YOLO 网络，以增强全局感受野。

> 本仓库是 [ClassInsight](https://github.com/MkmCv/ClassInsight) 课堂行为智能分析系统的**算法侧**，独立维护；系统侧（前后端）见该仓库。

---

## ✨ 主要特性

- **vHeat 集成**：基于热传导算子（DCT/IDCT）的全局感受野增强，模块即插即用。
- **完整工具链**：训练（`train.py`）、评估（`eval.py`）、环境自检（`check_environment.py`）。
- **可配置**：通过 YAML 调整 `time_step`、`base_size`、`e` 等热传导参数。
- **可编辑安装**：以 `pip install -e .` 方式安装定制版 ultralytics。

---

## 📦 目录结构

```
YOLO-vHeat/
├── README.md                # 项目说明（本文件）
├── docs/                    # 文档
│   ├── README.md            # 文档索引
│   ├── usage.md             # 完整使用文档（环境/数据/训练/评估/FAQ）
│   └── vheat-integration.md # vHeat 集成技术细节
├── pyproject.toml           # 包配置（可编辑安装）
├── requirements.txt         # 依赖
├── train.py                 # 训练 / 续训脚本
├── eval.py                  # 评估脚本
├── check_environment.py     # 环境自检
└── ultralytics/             # 二次开发的 ultralytics（含 vHeat 模块）
```

---

## 🔧 快速开始

### 1. 创建环境并安装依赖

```bash
conda create -n yolov12-vheat python=3.10
conda activate yolov12-vheat

# 按 CUDA 版本安装 PyTorch（示例 CUDA 12.1）
pip install torch==2.1.0 torchvision==0.16.0 --index-url https://download.pytorch.org/whl/cu121

# 以可编辑模式安装定制 ultralytics
pip install -e .
```

### 2. 环境自检

```bash
python check_environment.py
```

### 3. 训练

```bash
python train.py --data path/to/dataset.yaml \
                --model ultralytics/cfg/models/v12/yolov12.yaml \
                --epochs 300 --batch 16 --imgsz 640 --device 0
```

### 4. 评估

```bash
python eval.py --model runs/train/vheat/weights/best.pt \
               --data path/to/dataset.yaml --device 0
```

更详细的数据集准备、参数说明与常见问题，见 [docs/usage.md](docs/usage.md)。

---

## 📚 文档

| 文档 | 说明 |
|------|------|
| [docs/usage.md](docs/usage.md) | 完整使用文档：环境、数据集、训练、评估、FAQ |
| [docs/vheat-integration.md](docs/vheat-integration.md) | vHeat 集成技术细节与代码改动说明 |

---

## 📝 说明

- 训练产出的权重（`*.pt`/`*.pth`）、数据集、`runs/` 等不纳入版本控制（见 `.gitignore`）。
- 系统侧后端通过 `pip install -e .` 引用本项目的 ultralytics 包；若本项目移动了位置，需重新执行可编辑安装。

---

## 🙏 致谢

- [Ultralytics](https://github.com/ultralytics/ultralytics) — 基础检测框架
- [vHeat](https://github.com/MzeroMiko/vHeat) — 热传导算子实现

---

## 📄 许可证

本项目基于 [ultralytics](https://github.com/ultralytics/ultralytics)（AGPL-3.0）二次开发，遵循 **AGPL-3.0** 许可证，详见 [LICENSE](LICENSE)。
