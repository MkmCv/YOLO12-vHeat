# YOLO-vHeat

YOLOv12 集成 **vHeat**（基于热传导算子的视觉骨干）的目标检测框架，用于课堂教学行为识别。本项目在 [ultralytics](https://github.com/ultralytics/ultralytics) 基础上二次开发，将 vHeat 模块（如 `C2fHeat`）集成进 YOLO 网络，以增强全局感受野。

> 本仓库是 ClassInsight 课堂行为智能分析系统的**算法侧**，独立维护；系统侧（前后端）见另一个仓库。

---

## ✨ 主要特性

- **vHeat 集成**：基于热传导算子的全局感受野增强，模块即插即用。
- **完整工具链**：训练（`train.py`）、评估（`eval.py`）、环境自检（`check_environment.py`）。
- **可编辑安装**：以 `pip install -e .` 方式安装定制版 ultralytics。

---

## 📦 目录结构

```
YOLO-vHeat/
├── README.md                          # 本说明
├── README_vHeat.md                    # 详细使用文档（环境/数据/训练/评估）
├── MIGRATION_GUIDE.md                 # 从标准 YOLO 迁移指南
├── vHeat_Integration_Documentation.md # vHeat 集成技术文档
├── pyproject.toml                     # 包配置（可编辑安装）
├── requirements.txt                   # 依赖
├── train.py                           # 训练脚本
├── eval.py                            # 评估脚本
├── check_environment.py               # 环境自检
└── ultralytics/                       # 二次开发的 ultralytics（含 vHeat 模块）
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
python eval.py
```

更详细的数据集准备、参数说明与常见问题，见 [README_vHeat.md](./README_vHeat.md)。

---

## 📚 相关文档

- [README_vHeat.md](./README_vHeat.md) — 完整使用文档
- [MIGRATION_GUIDE.md](./MIGRATION_GUIDE.md) — 迁移指南
- [vHeat_Integration_Documentation.md](./vHeat_Integration_Documentation.md) — vHeat 集成技术细节

## 📝 说明

- 训练产出的权重（`*.pt`/`*.pth`）、数据集、`runs/` 等不纳入版本控制（见 `.gitignore`）。
- 系统侧后端通过 `pip install -e .` 引用本项目的 ultralytics 包；若本项目移动了位置，需重新执行可编辑安装。
