# python3 基础环境搭建（有点奇怪）

## 简单介绍

* python3的开发环境其实已经很容易搭建了吧，写那个就太没意思了，因此，这次搭建的python3开发环境有点特殊，因为本人想体验一下VS Code下开发Sanic程序，所以使用wsl，因为windows10默认商店下载的debian版本会有点高，所以遇到一些问题，本文主要是记录用途，为了应对以后开发python程序，可能会出现某些包仅能在Linux使用的场合；以及和生产环境统一。

## 步骤

* 前提:Windows 10 ，启动适用于Linux的Windows子系统,已经开启了bios的虚拟化开关，应用商店安装的debian，VS Code，我默认你已经完成了新系统的初始化操作（千万不要改源地址）

* VS Code安装Remote - WSL插件 完成后重启VS Code，点击左下角的绿色图标，随后选择Remote-WSL:New Window

* 到这里，其实你的Linux开发环境已经完成了，你写的代码，依赖的sdk都会是Linux子系统的环境，而不是Windows。

* ctrl + j 进入终端，可以看到目录已经是Linux的了。

* 接下来就是常规操作：`sudo apt-get update`，`sudo apt-get upgrade`

* 因为这种途径下载的系统一般比较新，换了源地址会造成各种软件版本不对，用默认就行。

* 安装aptitude（以防万一）：`sudo apt-get install aptitude`

* 安装python3：`sudo aptitude install python3`

* 安装python3-pip：`sudo aptitude install python3-pip` (tomorrow~)

* 完成了python3环境的搭建，重启VS Code，这个时候按理说右下角会提示你安装Python插件。安装完毕后再次重启VS Code 就能看到左下角显示了你在Linux环境的Python版本。

* 这时，你的Python3 wsl环境已经搭建完成，已经可以在这里开发后端程序了，并且调试/运行在Linux子系统，也不需要担心兼容性问题了。

* 最后安装Sanic：如果我们这里用正常的`sudo pip3 install sanic`依赖下载到一半，就会断掉。如果你的网络环境比较优秀，可能不会吧。这里可以用临时方案`sudo pip3 install sanic -i https://pypi.mirrors.ustc.edu.cn/simple/`(这里用了中科大的pip源)

* 到这里你的sanic依赖已经安装好了。

* 写个demo测试下吧：
  
  ```bash
  cd
  mkdir demos
  vim hello.py
  ```

* hello.py：

  ```python
  from sanic import Sanic
  from sanic.response import json
  app = Sanic()
  @app.route("/")
  async def hello_sanic(request):
    data = json({"msg":"hello world"})
    return data
  if __name__ == "__main__":
    app.run(host="0.0.0.0",port=5000)
  ```

* F5 调试
