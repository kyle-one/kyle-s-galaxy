---
{"dg-publish":true,"permalink":"/MyNote/Permanent/从零开始WSL2配置ubuntu18.04环境/"}
---

## 步骤

查看分发列表 `wsl --list --online`
安装 `wsl --install -d Ubuntu-18.04`
配置代理
```text
nano ~/.profile
```
在文件末尾粘贴以下内容：
```text
# set proxy
proxy=http://$(cat /etc/resolv.conf |grep -oP '(?<=nameserver\ ).*'):7890
export http_proxy=$proxy
export https_proxy=$proxy
export all_proxy=$proxy
export ALL_PROXY=$proxy
export no_proxy="localhost,127.0.0.1"
```
让设置立刻生效：
```text
source ~/.profile
```
测试一下是否能访问google
```
curl google.com
```
更新apt
```
sudo apt update
sudo apt upgrade
```
安装make等
```
apt install build-essential
```
安装python3.10 apt安装失败
```
sudo apt install python3.10
```
安装python3.10的依赖项
```
sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev
```
从官网下载源文件
```
sudo wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz
```
解压以及安装
```
tar -zvxf Python-3.10.0.tgz
cd Python-3.10.0/
./configure --enable-optimizations
make altinstall
```
太慢了，我自己安装了python3.8
切换python版本
```
update-alternatives --list python

sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.8 1

sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.8 1

```

## 安装
## 参考
- 设置代理：[超详细的wsl2下配置Ubuntu教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/600519231?utm_id=0)
- 其他：
	- [为 WSL2 一键设置代理 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/153124468)
	- [WSL2(Ubuntu20.04) window11 使用clash 配置 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/641260642?utm_id=0)
	- [WSL2 的开发环境配置 (基础配置, 网络代理, CUDA, Python, Fortran, Latex, 服务器配置) - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/619775346)
- 安装Oyenet，失败
	- [如何安装和使用 Oyente — 智能合约分析器 |作者：塔伦·库马尔·贾纳马迪 |硬币僧侣 |中等 (medium.com)](https://medium.com/coinmonks/how-to-install-and-use-oyente-a-smart-contract-analyzer-5251731e4aab)
- 安装docker
	- [2022最新 Docker 和 WSL2 ，炼丹环境配置指南 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/543280130)
- 使用docker安装Oyente
	- [enzymefinance/oyente: An Analysis Tool for Smart Contracts (github.com)](https://github.com/enzymefinance/oyente)
- ubuntu切换python版本
	- [ubuntu切换python版本_高旭的旭的博客-CSDN博客](https://blog.csdn.net/weixin_47540149/article/details/132245529)