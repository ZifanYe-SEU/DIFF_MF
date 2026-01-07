# DIFF-MF: A Difference-Driven Channel-Spatial State Space Model for Multi-Modal Image Fusion 

[![arXiv](https://img.shields.io/badge/arXiv-Paper-<COLOR>.svg)](https://arxiv.org/abs/xxxx.xxxxx)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Framework](https://img.shields.io/badge/PyTorch-%3E%3D2.1.0-orange)](https://pytorch.org/)
[![Stars](https://img.shields.io/github/stars/[GithubUsername]/[RepoName].svg?style=social)](https://github.com/[GithubUsername]/[RepoName])

This repository contains the official PyTorch implementation of the paper:
**"DIFF-MF: A Difference-Driven Channel-Spatial State Space Model for Multi-Modal Image Fusion"** 
<!-- TODO:(Accepted by [会议/期刊名称, e.g., CVPR 2025 / IEEE TNNLS]) -->
> **Authors**: Yiming Sun, Zifan Ye, Qinghua Hu, Pengfei Zhu

> **Affiliation**: the School of Automation, Southeast University, Nanjing, the School of Artificial Intelligence, Tianjin University, Tianjin

## 📢 News
<!-- TODO:- **[2026-01-07]**: Code and pre-trained models are released!) -->
<!-- TODO:- **[Date]**: The paper is accepted by [Conference/Journal].) -->
## 📜 Abstract
Multi-modal image fusion aims to integrate complementary information from multiple source images to produce high-quality fused images with enriched content. Although existing approaches based on state space model have achieved satisfied performance with high computational efficiency, they tend to either over-prioritize infrared intensity at the cost of visible details, or conversely, preserve visible structure while diminishing thermal target salience. To overcome these challenges, we propose DIFF-MF, a novel difference-driven channel-spatial state space model for multi-modal image fusion. Our approach leverages feature discrepancy maps between modalities to guide feature extraction, followed by a fusion process across both channel and spatial dimensions. In the channel dimension, a channel-exchange module enhances channel-wise interaction through cross-attention dual state space modeling, enabling adaptive feature reweighting. In the spatial dimension, a spatial-exchange module employs cross-modal state space scanning to achieve comprehensive spatial fusion. By efficiently capturing global dependencies while maintaining linear computational complexity, DIFF-MF effectively integrates complementary multi-modal features. Experimental results on the driving scenarios and low-altitude UAV datasets demonstrate that our method outperforms existing approaches in both visual quality and quantitative evaluation.

![Network Architecture](framework.png)
*Figure 1: The overall architecture of our proposed DIFF-MF.*

## 🔨 Requirements
The code has been tested with Python 3.8 and PyTorch 2.1.0

```bash
# 1. Create a conda environment
conda create -n diffmf python=3.8
conda activate diffmf

# 2. Install main dependencies
conda install cudatoolkit==11.8 -c nvidia
pip install torch==2.1.1 torchvision==0.16.1 torchaudio==2.1.1 --index-url https://download.pytorch.org/whl/cu118

# 3. Install mamba
# you should first download the offical whl of mamba form the https://github.com/state-spaces/mamba/releases and https://github.com/Dao-AILab/causal-conv1d/releases
# then use pip to install the whl you downloaded just now
# then run the command below
cd selective_scan
pip install .

# 4. Install other dependencies
pip install -r requirements # note that some packages may need to be install dependently
```

## 📂 Data Preparation
Please organize your dataset as follows. Note: Ensure that the Visible and Infrared images are strictly aligned (registered) and have the same filenames.

```
Project_Root/
├── dataset/
│   ├── train/
│   │   ├── M3FD/           
│   │   │   ├── vi/   # Visible images (Grayscale or RGB) 
│   │   │   │   ├── 1.jpg
│   │   │   │   └── ...
│   │   │   └── ir/
│   │   │   │   ├── 1.jpg
│   │   │   │   └── ...
│   │   └── ...     
│   └── test/
│       ├── TNO/            # Test Dataset 1
│       │   ├── vi/
│       │   └── ir/
│       └── MSRS/           # Test Dataset 2
│           ├── vi/
│           └── ir/
```

## 🚀 Usage
Train models
```
python -m torch.distributed.launch --nproc_per_node=2 --master_port=1234 train_DIFFMF.py --opt options/DIFFMF/DIFFMF.json  --dist True
```
Test models
```
python test_DIFFMF.py --model_path=./ckpt --iter_number=48000 --dataset=VIF --A_dir=ir  --B_dir=vi
```

<!-- TODO:## 📊 Results -->
<!-- TODO:## 🤝 Citation -->
<!-- TODO:## 📧 Contact -->






