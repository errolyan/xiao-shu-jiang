---
title: hts sinsy音源训练方法
tags: sinsy,音源训练,hts
grammar_cjkRuby: true
---
## hts 训练包
### 1.环境配置
```
 sudo apt-get install libx11-dev:i386
 sudo apt-get install libc6-dev:i386
 sudo apt-get install libx11-dev:i386 libx11-dev
 sudo apt-get install g++-multilib
 sudo apt-get install osspd
 sudo apt install git csh libx11-dev cmake gcc g++ automake
```
### 2.安装包官方下载地址
tips：下载安装HTK(先去 http://htk.eng.cam.ac.uk/register.shtml 注册)
原文: http://gloomyghost.com/2018/08/16/htstrain.html
[SPTK-3.9]( http://sp-tk.sourceforge.net/)
[HTS-2.3](http://hts.sp.nitech.ac.jp/)
[ hts_engine API:-1.10](http://hts-engine.sourceforge.net/)


If you use STRAIGHT, MATLAB and STRAIGHTV40 are required.
[STRAIGHT: ](http://www.wakayama-u.ac.jp/~kawahara/STRAIGHTtrial/)

### 3.0成功的包
百度网盘地址：https://pan.baidu.com/s/1i6huEaD  （成功的)2）

### 3.下载文件包（未成功的包1）
```
git clone https://gitee.com/GloomyGhost/SinsyVoiceCreat.git

```
### 开始安装依赖环境包
#### 安装htk
[教程地址]  http://gloomyghost.com/2018/08/16/htstrain.html)
```
sudo sh install_htk.sh
```
####  hts_engine_API
```
./configure
make all
make install
===========================================
cd hts_engine_API
./configure
make && sudo make install
cd ../
```
#### 安装SPTK
```
./configure
make
make install
================================================
cd SPTK
./configure
make && sudo make install
cd ../
```
#### 安装HTS for HTK
```
cd HTS_for_HTK/htk
make clean
./configure
make && sudo make install
cd ../
```
#### hts-train-demo
然后打开hts-train-demo文件夹，打开data，替换相应文件
raw文件夹为音频文件，格式为：480000Hz Little Endian 跳过前2位
可以使用ffmpeg进行转换：
```
ffmpeg -i input.wav -f s16le -ar 48000 -acodec pcm_s16le output.raw
```
label/full放入音乐的完整label，可以用Sinsy导出
```
sinsy -x dic -m jp.htsvoice -w c -o output.lab -l infile.xml
```
-x 指定发音表所在文件夹
-m 指定任意一个htsvoice（不影响输出结果，必须指定一个htsvoice是bug）
-w 指定语言，j代表日语 c 代表中文
label/mono指定的歌词和对应时间，元音和辅音要拆开来，时间一定要准确，否则影响音源合成效果
#### 具体怎么写可以参照官方的例子

#### 开始训练
```
screen -S train  #后台训练
cd HTS-train-demo
./configure --with-hts-search-path=../HTS_for_HTK/htk/HTKTools
make all
```
#### 训练结果
```
#查看训练进度
perl scripts/Training.pl 当前的绝对路径/scripts/Config.pm
```
1.在voice文件夹里
2.大约需要八小时的训练时间