# linux-config

搭建linux环境常用到的一些操作配置一个环境的常用操作

# WSL2 环境配置
[wsl2][https://docs.microsoft.com/zh-cn/windows/wsl/install-win10]

```
# WSL 安装 https://docs.microsoft.com/zh-cn/windows/wsl/install-win10

# step1 启用子系统
# powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

# step2 更新到wsl2
# x64 需要更新到1903以上版本(内部版本18362以上)
# windows 更新助手 : https://www.microsoft.com/software-download/windows10 

# step3 启用虚拟机功能
# powershell 管理员模式
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

# step4 Linux 查看内核并更新 
# 查看内核 powershell 
systeminfo | find "System Type"
# 下载地址
# x64 http://aka.ms/wsl2kernelmsix64
# ARM http://aka.ms/wsl2kernelmsiarm64

# step5 WSL2 设置为默认
# powershell
wsl --set-default-version 2


# WSL 切换默认登陆用户 PowerShell
C:\Users\$UserName\AppData\Local\Microsoft\WindowsApps\ubuntuXXXX.exe config --default-user root

# WindowsTerminal 修改配置
# ctrl+, 打开配置文件, 更详细的见WinTerminal.json

# PS: WSL清理vhdx
# windows cmd 管理员权限下
wsl --shutdown
diskpart
select vdisk file="C:\WSL-Distros\…\ext4.vhdx"
attach vdisk readonly
compact vdisk
detach vdisk
exit

```

# 
```
{
    "defaults":
        {
            "fontSize": 16,
            "fontFace": "Cascadia Mono",
            "antialiasingMode": "grayscale",
            "cursorShape": "bar",
            "cursorColor": "#00ddff",
            "cursorHeight": 50
        },
    "list": 
    [
        {
            "guid": "{c6eaf9f4-32a7-5fdc-b5cf-066e8a4b1e40}",
            "hidden": false,
            "name": "Ubuntu-18.04",
            "source": "Windows.Terminal.Wsl",
            "colorScheme": "FrostMine",
            "cursorColor": "#000000",
            "cursorShape":"bar",
            "startingDirectory": "//wsl$/Ubuntu-18.04/root/",
            "useAcrylic": true,
            "acrylicOpacity" :1.0,
            "padding": "10,10,10,10"
         }
    ],
    "schemes": [    
        {       
            "name" : "FrostMine",
            "cursorColor": "#000000",
            "selectionBackground": "#000000",
            "background" : "#CCE8CF",
            "foreground" : "#000000",
            // 黑蓝青绿紫红白黄 
            "black" : "#0C0C0C",
            "red" : "#C50F1F",
            "green" : "#16C60C",
            "yellow" : "#8B4513",
            "blue" : "#0095FF",
            "purple" : "#9400D3",
            "cyan" : "#3A96DD",
            "white" : "#CCCCCC",
            "brightBlack" : "#767676",
            "brightRed" : "#E74856",
            "brightGreen" : "#16C60C",
            "brightYellow" : "#8B4513",
            "brightBlue" : "#0095FF",
            "brightPurple" : "#B4009E",
            "brightCyan" : "#61D6D6",
            "brightWhite" : "#F2F2F2"
        }
    ],
    "keybindings":
    [
        // dutbyy adding
        { "command": "toggleFullscreen", "keys": "alt+enter" },
        { "command": "duplicateTab", "keys": "alt+t" },
        { "command": "nextTab", "keys": "ctrl+tab" },
        { "command": "closeTab", "keys": "alt+w" },
        { "command": { "action": "switchToTab", "index": 0 }, "keys": "alt+1" },
        { "command": { "action": "switchToTab", "index": 1 }, "keys": "alt+2" },
        { "command": { "action": "switchToTab", "index": 2 }, "keys": "alt+3" },
        { "command": { "action": "switchToTab", "index": 3 }, "keys": "alt+4" },
        { "command": { "action": "switchToTab", "index": 4 }, "keys": "alt+5" },
        { "command": { "action": "switchToTab", "index": 5 }, "keys": "alt+6" },
        { "command": { "action": "switchToTab", "index": 6 }, "keys": "alt+7" },
        { "command": { "action": "switchToTab", "index": 7 }, "keys": "alt+8" },
        { "command": { "action": "switchToTab", "index": 8 }, "keys": "alt+9" },
        { "command": {"action": "copy", "singleLine": false }, "keys": "alt+c" },
        { "command": "paste", "keys": "alt+v" },
        { "command": "find", "keys": "alt+f" },
        { "command": { "action": "adjustFontSize", "delta": 1 }, "keys": "alt+=" },
        { "command": { "action": "adjustFontSize", "delta": -1 }, "keys": "alt+-" }
    ]
}
```
# Linux 配置(Ubuntu为例)

## 1. apt源

以 ubuntu的清华源为例
[ubuntu-apt][https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/]

```
# 16.04 LTS 
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
# 18.04 LTS
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# 20.04 LTS 
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

```

## 2. docker
建议开发时使用docker环境测试[使用-v pathA:pathB 映射]  这样比较好管理运行环境的依赖, 也方便后期打包

[docker-practice][https://yeasy.gitbook.io/docker_practice/]

```
1. 安装
apt remove docker docker.io docker-engine
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh --mirror Aliyun

2. 修改daemon.json
# 启动后, vim /etc/docker/daemon.json
# 这个根据自己的需求修改, 修改后需要重启docker生效
{
    "registry-mirrors": [
        "http://f1361db2.m.daocloud.io"
    ],
    "insecure-registries": [
        "registry.inspir.ai:5000"
    ],
    "debug": true,
    "experimental": false
}
# /etc/hosts 增加 
192.168.2.100       registry.inspir.ai
42.62.26.201        gitlab.inspir.ai
```


## 3. python
```
# 系统依赖库
	apt install -y
	libbz2-dev gcc make zlib1g-dev libsqlite3-dev python3-dev libxml2-dev libffi-dev libssl-dev libxslt-dev 
	vim wget curl tar xz-utils
# 下载指定版本, 以3.6.8 为例, 此处使用了华为的镜像
    wget -O  Python-3.6.8.tar.xz http://mirrors.huaweicloud.com/python/3.6.8/Python-3.6.8.tar.xz 
# 安装 
    ./configure  --enable-optimizations 
    make && make install 
# pip 源切换 ~/.pip/pip.conf
  1.   
    [global]
    index-url=https://pypi.tuna.tsinghua.edu.cn/simple
  2. 
    pip3 config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
# 安装grpc的库, 一般都会使用到
    pip3 install grpcio protobuf \
```

## 4. kubectl client
```
# 使用下面命令下载最新的发行版本：
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.19.0/bin/linux/amd64/kubectl
# 标记 kubectl 文件为可执行：
chmod +x ./kubectl
# 将文件放到 PATH 路径下：
sudo mv ./kubectl /usr/local/bin/kubectl
# 查看版本
kubectl version --client
# 配置kubectl conf
vim ~/.kube/config
```

## 5. Grpc

```
0. 准备工作
git clone github.com/google/grpc 
apt install -y  build-essential autoconf git pkg-config &\
		automake libtool curl make g++ unzip cmake vim perl

0.5 [可能需要安装openssl-1.1]
cd //openssl-1.1xx
./config shared && make && make install && make clean && ldconfig

1. 安装protobuf
cd /third_party/protobuf
./autogen.sh && ./configure --enable-shared 
make && make check && make install && make clean && ldconfig

2. 安装grpc
cd //grpc
make && make install && make clean && ldconfig 

3. 安装absl
mkdir build && cd build 
cmake .. -DBUILD_SHARED_LIBS=ON -DCMAKE_CXX_STANDARD=11 
make && make install && make clean && ldconfig 
```

## 6. 
