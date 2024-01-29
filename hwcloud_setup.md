# 华为云ECS 设置

## 购买和设置
### 一. 购买华为云ECS  

1. 计费方式：按需计费
2. 区域：拉美-墨西哥城二
3. 实例类型：GPU加速型pi2
4. 镜像选择：Ubuntu with Tesla Driver and Cuda
<img width="648" alt="image" src="https://github.com/wgxgg/LLM-quickstart/assets/157986938/02bae645-b2dd-4825-887e-488d7c3ddaf6">

（本区目前只有16，其它拉美区好像有18）

### 二. 开通弹性公网IP，绑定到ECS 实例  
否则ECS 实例不仅无法被外网访问（Jupyter 和SSH 所需），也无法访问外网（下载驱动和模型、拉取和推送代码所需）

### 三. 升级Ubuntu 到 20 或 22  
以原版本16为例，升级到20，需要两次。因为Ubuntu 的官方升级工具，每次执行只能升级到下一个LTS 版本，不允许跨LTS 版本升级。

### 四. 安装T4 显卡的最新驱动 
最新版本（截至2024-01-29）的驱动下载链接是： https://us.download.nvidia.com/tesla/535.154.05/NVIDIA-Linux-x86_64-535.154.05.run  

地址可在官网页面自行获取：  
![image](https://github.com/wgxgg/LLM-quickstart/assets/157986938/8671e9cc-b264-47ac-88bb-7cbb068e7021)

### 五. 安装CUDA 最新版本  

<img width="743" alt="image" src="https://github.com/wgxgg/LLM-quickstart/assets/157986938/9e6790d2-4cf0-4b5c-b247-c103d6a08512">

按顺序安装Base Installer 和 Driver Installer。

注意：红线处的版本号，需替换为第四步中显卡驱动的版本号，如`535.154.05`。详见：https://docs.nvidia.com/cuda/cuda-installation-guide-linux/#ubuntu


### 快捷通道
步骤三至步骤五，可使用本人制作的镜像
`Ubuntu 22.04 server 64bit with Tesla Driver 535.154.05 and Cuda 12.3`



使用“拉美-墨西哥城二”区的tx，需要镜像的，可以按照[该文档](https://support.huaweicloud.com/usermanual-ims/zh-cn_topic_0032042418.html)，拿到自己对应“拉美-墨西哥城二”的“项目ID”后发给我（wx: xixiao）。

如果使用的是其它区，暂不支持镜像共享。

## 使用
不用的时候可以关机，可以减少支出。关机后仅计算磁盘占用费用。

<img width="334" alt="image" src="https://github.com/wgxgg/LLM-quickstart/assets/157986938/093a5efc-4829-4194-879d-43c371bbf1b5">  

公网IP费用，所在区（拉美-墨西哥城二）目前的规则是，如果IP已绑定到ECS，则不会收取。其它区未知。
