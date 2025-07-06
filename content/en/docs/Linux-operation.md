---
title: Linux Operation
slug: Linux-Operation
lastmod: 2025-07-01T00:00:00+00:00
---

## 简单

```powershell
# 管理员权限操作
sudo

# 进入某个文件夹
cd

# 进入上层目录
cd ..

# 查看当路径
pwd

# ip address
ifconfig

# 列出文件夹里的所有文件
ls    不包括隐藏文件
ls -a  包括隐藏文件

把某个文件移动到某个文件夹
mv filename /usr/java

# 创建文件或文件夹
mkdir music    在当前目录创建目录music
touch test.txt 将test.txt 的时间改为当前时间，文件不存在则新建

# 删除文件或文件夹
rm filename 删除文件
rm -d dirname 删除空文件夹
rm -r dirname 删除非空文件夹

# java版本
java -version

# vim 查看文件
sudo vim /path/file
编辑退出编辑：i -> esc
退出：:q
退出保存：:wq
退出不保存：:q!

# 退出
ctrl+c 向当前进程发送 SIGINT 信号，用于终止一个进程
ctrl+z 向当前进程发送 SIGSTOP 信号，用于挂起一个进程
```

## 复杂

```powershell
# 授予执行权限，授予之后会变绿色
chmod +x

# 切换 java 版本
sudo update-alternatives --config java
java --version

# 添加环境变量
export PATH=$PATH:/home/caiyizhang
export PATH=/home/caiyizhang:$PATH
export PATH=`pwd`:$PATH

# 查看环境变量
echo $PATH

# Linux 下文件颜色的含义
蓝色目录，绿色可执行文件，红色压缩文件，浅蓝色链接文件
灰色其它文件，红色闪烁链接的文件有问题，黄色设备文件

# CURL 用来与服务器之间传输数据的工具
GET请求：curl URL?a=1&b=nihao 
POST请求：curl -H "Content-Type: application/json" -X POST -d '{"abc":123,"bcd":"nihao"}' URL

# grep 查找文件里符合条件的字符串或正则表达式
grep hello file.txt  在文件 file.txt 中查找字符串 "hello"，并打印匹配的行

# 查找文件 
find -name "build.xml"

# apt Ubuntu 中的 Shell 前端软件包管理器
sudo apt update  列出所有可更新的软件
sudo apt upgrade 升级软件包
sudo apt install <package_name>  安装指定的软件
sudo apt remove <package_name>  移除指定的软件
```