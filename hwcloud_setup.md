# 华为云ECS 设置

- 购买和设置
- 使用


## 购买和设置
### 一. 购买华为云ECS  

1. 计费方式：按需计费
2. 区域：拉美-墨西哥城二
3. 实例类型：GPU加速型pi2
4. 镜像选择：Ubuntu with Tesla Driver and Cuda
（本区目前只有16，其它拉美区好像有18）
4. 系统盘：SSD 500GB（老师建议）

![image](https://github.com/wgxgg/LLM-quickstart/assets/157986938/cee27926-d1ef-4156-bd30-4a58a74c077b)


### 二. 开通弹性公网IP，绑定到ECS 实例  
否则ECS 实例不仅无法被外网访问（Jupyter 和SSH 所需），也无法访问外网（下载驱动和模型、拉取和推送代码所需）

![image](https://github.com/wgxgg/LLM-quickstart/assets/157986938/aa224b1e-f663-4463-a065-bf9e5a00b110)

### 三. 升级Ubuntu 到 20 或 22  
以原版本16为例，升级到20，需要两次。因为Ubuntu 的官方升级工具，每次执行只能升级到下一个LTS 版本，不允许跨LTS 版本升级。

### 四. 安装T4 显卡的最新驱动 
最新版本（截至2024-01-29）的驱动下载链接是： https://us.download.nvidia.com/tesla/535.154.05/NVIDIA-Linux-x86_64-535.154.05.run  

地址可在官网页面自行获取：  
https://www.nvidia.com.tw/Download/index.aspx?lang=tw
![image](https://github.com/wgxgg/LLM-quickstart/assets/157986938/8671e9cc-b264-47ac-88bb-7cbb068e7021)

### 五. 安装CUDA 12.2  

下载和安装
<img width="1020" alt="image" src="https://github.com/wgxgg/LLM-quickstart/assets/157986938/3c580a8d-66dd-44a3-b667-c31372381541">

### 快捷通道
步骤三至步骤五，可使用本人制作的镜像
`Ubuntu 22.04 server 64bit with Tesla Driver 535.154.05 and Cuda 12.2`

使用“拉美-墨西哥城二”区的tx，需要镜像的，可以按照[该文档](https://support.huaweicloud.com/usermanual-ims/zh-cn_topic_0032042418.html)，拿到自己对应“拉美-墨西哥城二”的“项目ID”后发给我（wx: xixiao）。

如果使用的是其它区，暂不支持镜像共享。

镜像说明：
1. `~/LLM-quickstart` 是项目目录。提交代码前，先添加自己的remote: `git remote add origin <your repo url>`
2. 使用 pyenv 设置了Python 的全局版本为 3.11.7
3. 项目使用的virtualenv 可通过 `pyenv activate venv-3.11.7` 激活。项目所需的依赖已安装在该virtualenv 中（by pip）
4. Jupyter Lab 已安装（global）
5. 磁盘快满了。`~/` 目录下有些下载的显卡驱动和CUDA Tookit的文件，以及练习时，选了一些较大的模型，可以手动删除。  
附上扩容的命令： https://support.huaweicloud.com/usermanual-evs/evs_01_0072.html （同学@大伟 提供）

## 使用
不用的时候可以关机，可以减少支出。关机后仅计算磁盘占用费用。

<img width="334" alt="image" src="https://github.com/wgxgg/LLM-quickstart/assets/157986938/093a5efc-4829-4194-879d-43c371bbf1b5">  

公网IP费用，所在区（拉美-墨西哥城二）目前的规则是，如果IP已绑定到ECS，则不会收取。其它区未知。
