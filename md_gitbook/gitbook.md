# 搭建GitBook
 这边文章会介绍如何安装GitBook以及基于Git、GitHub建立属于自己的静态博客。
 现在开始的是搭建一个最基础的工作环境，不会新建任何工程外的文件。

## 安装 node.js安装 
 点击[Node.js](https://nodejs.org)下载安装即可，最新版已自带npm。

## 安装配置GitBook 
* 安装完node.js后在终端（或者cmd、PowerShell）输入:
    ```bash 
    npm install -g gitbook-cli
    ```
* 安装完成后，新建并进入目录:                                                                                 
    ```bash 
    mkdir mybook
    cd mybook
    ```
* 初始化gitbook：
    ```bash 
    gitbook init
    ```
* 启动gitbook环境：
    ```bash 
    gitbook serve
    ```
* 到这里有已经完成了本地的GitBook的搭建以及启动了
  点击进入:[localhost:4000](http://localhost:4000)

## 安装 Git 
  还是进入官网[Git官网](https://git-scm.com)
  下载Git，选好安装路径一路next就可以了
 
## 绑定GitHub到本地Git 

## 搭建基于GitBook的静态网站