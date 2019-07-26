# .Net Core开发环境搭建

## 下载 .net Core SDK

1. [官网下载](https://dotnet.microsoft.com/download)

2. 选择对应的平台，下载（Build Apps）推荐版本，生产环境运行则选择（Run Apps）

3. 安装，每个平台都会提供安装引导，可在官网查看，windows则是一路next

4. 当前选择的是Windows的普通SDK（不带Visual Studio 2017/2019的版本）

5. 选择使用Visual Studio Code进行开发，需要安装插件，当前版本只需要在Visual Studio Code安装C#插件就够了，等待安装，安装插件期间编辑器的左下角会出现Dowload ... 的提示，其实就是在安装.net core开发中需要的依赖。

6. 安装完毕后，创建hello world试下吧，使用编辑器自带的终端，进入并创建Hello World文件夹，输入：dotnet new console

7. dotnet run 终端输出Hello World!。

## 入门级别的内容

1. 入门内容都可以通过[官方文档](https://docs.microsoft.com)获取，微软已经做了多语言支持，应该是相当全的技术文档了。

2. 资源(Resources)
    * [核心文档 Core Documentation](https://aka.ms/dotnet-docs)
    * [SDK文档 SDK Documentation](https://aka.ms/dotnet-cli-docs)
    * [发行说明 Release Notes](https://aka.ms/20-p2-rel-notes)
    * [教程 Tutorials](https://aka.ms/dotnet-tutorials)
