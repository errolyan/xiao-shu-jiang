---
title: WuKonChatBot 
tags: WuKonChat,ubuntu,小书匠
grammar_cjkRuby: true
---


欢迎使用 **{小书匠}(xiaoshujiang)编辑器**，您可以通过 `小书匠主按钮>模板` 里的模板管理来改变新建文# 人脸唤醒
## 参考[snowboy](https://github.com/Kitt-AI/snowboy.git)
支持：linux、树莓派、moc 和windows
制作过程：
```
- 1.snowboy 唤醒模型制作：
- 2.环境安装：（ubuntu）
- 3.测试你的唤醒词
```
1. [snowboy 官网](https://snowboy.kitt.ai)
### 1.snowboy 唤醒模型制作：
```
1.官网申请账号，可github登陆
2. 选取一个唤醒词：比如老张
3. 按流程制作和录音：3次
4. 测试模型
5.下载模型：备用

```
### 2.环境安装：（ubuntu）
- SoX (audio conversion)
- PortAudio or PyAudio (audio capturing)
- SWIG 3.0.10 or above (compiling Snowboy for different languages/platforms)
- ATLAS or OpenBLAS (matrix computation)
```
#1.在ubuntu 16.04 下安装
#Access Microphone：
sudo apt-get install python-pyaudio python3-pyaudio sox
pip install pyaudio
#tip：测试硬件是否能够录音
rec temp.wav

```
### 3.swig环境安装
- swig版本需要：3.0.10 and以上
- [官网下载swig源文件](http://www.swig.org/survey.html)
- 
```
#1.安装g++依赖包()
sudo apt-get install g++
#2.ubuntu 环境下默认安装，终端输入一下命令，可以查看版本
g++ -version
#3.安装 pcre
sudo apt-get install libpcre3 libpcre3-dev
#4. 解压 swig 源码 
chmod 777 swig-3.0.12.tar.gz # 改变权限
tar -xzvf swig-3.0.12.tar.gz # 解压
#5. 配置、编译和安装 swig
#指定安装目录
./configure --prefix=/home/errolyan/swig/   
#编译
make
#安装
make install
# 6.配置安装路径
sudo vim /etc/profile
#将刚才的路径 /home/errolyan/swig/bin添加到profile文件的path下面：（文件最后几行）
export SWIG_PATH=/home/errolyan/swig/bin
export PATH=$SWIG_PATH:$PATH
#7.刷新环境
source /etc/profile
#8.测试swig
swig -version
#可以看到版本信息
```
### 4.Ubuntu 16.04 安装OpenBLAS步骤
```
git clone git://github.com/xianyi/OpenBLAS
 cd OpenBLAS
 sudo apt-get install gfortran
 sudo make FC=gfortran   #tips：gfortran --version 未有版本 需要安装 sudo apt-get install gfortran
 sudo make install
```
然后执行以下命令：
```
sudo ln -s /opt/OpenBLAS/lib/libopenblas.so.0   /usr/lib/libopenblas.so.0
```
查看版本信息
```
g++ --version
gcc --version
gfortran --version
```
结果gfortran也有，在目录/usr/lib/x86_64-linux-gnu/里面：
```
sudo ln -s /usr/lib/x86_64-linux-gnu/libgfortran.so.3 /usr/lib/libgfortran.so

编译例子：
gcc testOpenBlas.c  -I /opt/OpenBLAS/include/ -L/opt/OpenBLAS/lib -lopenblas
```
### 4.安装atlas和openblas（安装一个就可以）
```
#Then install the atlas matrix computing library:

sudo apt-get install libatlas-base-dev
```
## 测试你的唤醒词
添加你自己的模型文件到固定的路径：更改dome里面的自己的模型路径
```
#需要的文件结构为
├── README.md
├── _snowboydetect.so
├── demo.py
├── demo2.py
├── light.py
├── requirements.txt
├── resources
│   ├── ding.wav
│   ├── dong.wav
│   ├── common.res
│   └── snowboy.umdl
├── snowboydecoder.py
├── snowboydetect.py
└── version
```
## good luck章的内容。