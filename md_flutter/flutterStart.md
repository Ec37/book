# Flutter环境搭建

## 一.获取Flutter SDK
1. 环境变量配置（墙内用户不配置的话，下载依赖和Update的时候会非常痛苦）：
`PUB_HOSTED_URL=https://pub.flutter-io.cn`
`FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn`
2. 下载SDK项目（还有多种方法下载，只记录两种吧）：
`git clone -b beta https://github.com/flutter/flutter.git`
如果觉得时间长的话，可以试下到官网下载最新的Sdk：[Flutter官网下载](https://flutter.dev/docs/development/tools/sdk/releases#windows)
下载完成解压
3. Sdk路径配置到环境变量的Path：
`PATH=...;D:\*\flutter\`
4. 运行flutter doctor
检查环境需要的依赖，一般都会提示出来
`flutter doctor`

## 二.安装Android Studio(实际上就是安装Android SDK)
0. 下载安装就不说了
1. 不需要启动或者创建项目，找到configure->setting，搜索sdk，找到Android SDK，下载需要开发的Android版本对应的SDK
2. 下载完所需的Android SDK后，配置环境变量ANDRPID_HOME，找到Android SDK的路径即可
3. 安装完成后，再一次运行flutter doctor，将提示缺失的都配置完就可以了

## 三.Android Studio进行开发（无需进入 四.）
0. 找到configure->plugins
1. 安装flutter插件
2. 安装Dart插件
3. 这样就可以new Flutter project了

## 四.Visual Studio Code进行开发
1. 安装flutter插件
2. 安装Dart插件
3. ctrl+shift+p->输入flutter->选择New 
4. 可能会提示选择Flutter SDK路径
5. 输入项目名->选择保存路径->创建完成

## 五.在虚拟机运行/调试程序
1. 打开Android Stodio -> configure -> AVD Manager创建新的Android一般选择最新版的上一版就可以了，最新版本可能会不兼容调试（只能运行）
2. 点击▶启动
3. 虚拟机启动完后，打开编辑器（主要是VSCode，Android Stodio一般会自动打开虚拟机）,Run/Debug部署到虚拟机调试