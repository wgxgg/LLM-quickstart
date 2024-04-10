# DeepSpeed 框架安装指南

## 更新 GCC 和 G++ 版本（如需。Ubuntu 22.04 中，gcc/g++的版本已经高于7，为11.4.0，需跳过该步骤！）

首先，添加必要的 PPA 仓库，然后更新 `gcc` 和 `g++`：

```bash
sudo apt install software-properties-common
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt update
sudo apt install gcc-7 g++-7
```

更新系统的默认 `gcc` 和 `g++` 指向：

```bash
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 60 --slave /usr/bin/g++ g++ /usr/bin/g++-7
sudo update-alternatives --config gcc
```

## 创建隔离的 Anaconda 环境

如果想要隔离环境，建议采用 clone 方式，新建一个 DeepSpeed 专用的 Anaconda 环境：

```bash
conda create -n deepspeed --clone base
```

## 安装 Transformers 和 DeepSpeed

### 源代码安装 Transformers

遵循[官方文档](https://huggingface.co/docs/transformers/installation#install-from-source)，通过下面的命令安装 Transformers：

```bash
pip install git+https://github.com/huggingface/transformers
```

### 安装 Rust 编译器（maturin 需要）
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### 源代码安装 DeepSpeed

根据你的 GPU 实际情况设置参数 `TORCH_CUDA_ARCH_LIST`。NVIDIA Tesla T4 GPU 的计算能力（Compute Capability）是 7.5。NVIDIA GeForce RTX 4090 使用的是 NVIDIA 的最新Ampere 架构，其具体的计算能力（Compute Capability）为 8.9。

如果你需要使用 CPU Offload 优化器参数，设置参数 `DS_BUILD_CPU_ADAM=1`；如果你需要使用 NVMe Offload，设置参数 `DS_BUILD_UTILS=1`：

```bash
git clone https://github.com/microsoft/DeepSpeed/
cd DeepSpeed
rm -rf build
TORCH_CUDA_ARCH_LIST="8.9" DS_BUILD_CPU_ADAM=1 DS_BUILD_UTILS=1 pip install . \
--global-option="build_ext" --global-option="-j8" --no-cache -v \
--disable-pip-version-check 2>&1 | tee build.log
```

**注意：不要在本项目目录下 clone DeepSpeed 源代码安装，容易造成误提交。**

### 使用 DeepSpeed 训练 T5 系列模型

- 单机单卡训练脚本：[train_on_one_gpu.sh](train_on_one_gpu.sh)
- 分布式训练脚本：[train_on_multi_nodes.sh](train_on_multi_nodes.sh)
