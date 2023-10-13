---
{"dg-publish":true,"permalink":"/MyNote/Permanent/从零开始Ubuntu配置Oyente环境/"}
---

在 [[MyNote/Permanent/从零开始WSL2配置ubuntu18.04环境\|从零开始WSL2配置ubuntu18.04环境]] 后，进行该文的配置。
## 安装go1.7

从官网[All releases - The Go Programming Language](https://go.dev/dl/) 找到想要安装版本的链接
go下载到ubuntu
```sh
# 下载，其他版本在 https://go.dev/dl/ 中找到源链接
wget https://go.dev/dl/go1.7.linux-amd64.tar.gz
# 解压
sudo tar -C /usr/local -xzf go1.7.linux-amd64.tar.gz
# 软链接
sudo ln -s /usr/local/go/bin/* /usr/bin/
```
设置环境变量
```sh
sudo vim ~/.bashrc
```
在文件末尾添加
```sh
export GOPATH="$HOME/go"
export PATH="$PATH:/usr/local/go/bin:$GOPATH/bin"
export GOPROXY=https://goproxy.cn,direct
```
应用配置
```sh
source ~/.bashrc
```
检查版本
```sh
go version
```
安装solc。Oyente 目前只支持 0.4.19 以下的 solidity 版本
```sh
pip3 install solc-select
solc-select install 0.4.19
solc-select use 0.4.19
solc --version
```
中途报错
```sh
lyk@LAPTOP-G2IPOS6F:~$ solc-select install 0.4.19
Traceback (most recent call last):
  File "/usr/lib/command-not-found", line 28, in <module>
    from CommandNotFound import CommandNotFound
  File "/usr/lib/python3/dist-packages/CommandNotFound/CommandNotFound.py", line 19, in <module>
    from CommandNotFound.db.db import SqliteDatabase
  File "/usr/lib/python3/dist-packages/CommandNotFound/db/db.py", line 5, in <module>
    import apt_pkg
ModuleNotFoundError: No module named 'apt_pkg'
```
尝试解决
 [Linux - python-dev 安装错误：导入错误：没有名为 apt_pkg 的模块 - 堆栈溢出 (stackoverflow.com)](https://stackoverflow.com/questions/13708180/python-dev-installation-error-importerror-no-module-named-apt-pkg)
```shell
cd /usr/lib/python3/dist-packages/
sudo ln -s apt_pkg.cpython-36m-x86_64-linux-gnu.so apt_pkg.so
```
安装go-ethereum。Oyente 目前只支持 geth 1.7.3 和 evm 1.7.3
```sh
git clone https://github.com/ethereum/go-ethereum.git
cd go-ethereum 
# 切换分支
git checkout v1.7.3
#编译
make all
# 配置环境
sudo vim ~/.bashrc

#  增加 geth bin 目录到环境变量
# 以下路径根据实际安装路径进行修改
export PATH=$PATH:$HOME/go-ethereum/build/bin

# 退出并使修改命令生效
source ~/.bashrc

# 查看 geth 版本
geth version
```
安装z3，且Oyente 目前只支持 z3. 4.5.1
```sh
pip3 install z3-solver==4.5.1.0
```
安装crytic-compile 库，但 crytic-compile 库安装版本不可以超过 v0.1.13
```sh
pip3 install crytic-compile==0.1.13
```
出错
```sh
    Modules/_sha3/sha3module.c:18:10: fatal error: Python.h: No such file or directory
     #include "Python.h"
              ^~~~~~~~~~
    compilation terminated.
    error: command 'x86_64-linux-gnu-gcc' failed with exit status 1

    ----------------------------------------
Command "/usr/bin/python3 -u -c "import setuptools, tokenize;__file__='/tmp/pip-build-fmw88jqb/pysha3/setup.py';f=getattr(tokenize, 'open', open)(__file__);code=f.read().replace('\r\n', '\n');f.close();exec(compile(code, __file__, 'exec'))" install --record /tmp/pip-ketb4a0f-record/install-record.txt --single-version-externally-managed --compile --user --prefix=" failed with error code 1 in /tmp/pip-build-fmw88jqb/pysha3/
```
通过安装某个包解决
```sh
sudo apt-get install libpython3.8-dev
```
下载oyente
```sh
git clone https://github.com/enzymefinance/oyente.git
```
执行官网库的报错，原因不明
```sh
lyk@LAPTOP-G2IPOS6F:~/oyente/oyente$  python oyente.py -s greeter.sol
CRITICAL:root:Solidity compilation failed. Please use -ce flag to see the detail.
```
新建合约并且测试，成功
```sh
# 新建目录 
mkdir ~/test 
# 新建 .sol 智能合约 
vim ~/test/test.sol

#test.sol 合约
pragma solidity >=0.4.19;

contract test {
    function helloworld() pure public returns (string)
    {
        return "hello world";
    }
}

# 进入 oyente 目录 
cd ~/oyente/oyente 
# 评估本地合约 
python3 oyente.py -s ~/test/test.sol
```
- 参考
	- [Oyente：智能合约漏洞检测工具的安装与使用_mutou___的博客-CSDN博客](https://blog.csdn.net/mutou___/article/details/121584877)
	- [Oyente搭建，框架结构以及helloworld案例解析(一)_oyente原理-CSDN博客](https://blog.csdn.net/narcissus2_/article/details/115832793)
	- [[智能合约]Oyente安装配置 - 伶俐虫虫 - 博客园 (cnblogs.com)](https://www.cnblogs.com/xiao-xiaoyang/p/17370497.html)
	- [在Ubuntu上安装指定版本的Go语言 - 程序员YY的开发历程 (yqqy.top)](https://yqqy.top/ubuntu-install-golang/#%E5%AE%89%E8%A3%85)