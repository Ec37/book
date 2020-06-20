# 有效利用阿里云ddns服务(1) - 低成本服务器搭建


## 提前准备:
1. 阿里云购买的域名
2. 一台或者两台设备(ARM或者x86都行，Android能装Termux其实就可以，iOS估计要越狱)
3. 公网IP（电信打电话给客服就能免费申请到）
4. 提前下载好对应平台的jdk文件(ARM或者x86)
5. 查看自家光猫底部的贴纸获取：管理页地址、账号、默认密码 (路由器应该不用提吧)
6. 需要有Java和SpringBoot编程基础（就是调用一下阿里的API，可以使用其他语言，不深究）

## 确保自己的宽带已申请公网IP

1. 进入http://www.net.cn/static/customercare/yourIP.asp 查看自己的IP
2. Windows系统进入cmd/powershell输入: tracert <刚才获取的IP>
3. 如果显示两行，则很大概率说明是拥有公网IP的，因为目前运营商赠送的光猫，很多是和路由器一体的，如果你还接一个路由器就会显示两行
![tracert.png](resources\tracert.png)

## 根据情况设置光猫和路由器

### 仅光猫的情况:
1. 如果是只使用一个带局域网功能的光猫，其实要更简单，就是不怎么符合实际情况:
![仅光猫1.png](resources\仅光猫1.png)
![仅光猫2.png](resources\仅光猫2.png)

### 光猫+路由器：
1. 首先把映射到外网的设备设置为DMZ主机(路由器映射其实也行，还可以多台主机映射到外网，就是设置比较繁琐，有利有弊)，路由器设置完毕：
![dmzcf.png](resources\dmzcf.png)
2. 根据光猫底下的信息，进入到电信光猫的配置页面，进入高级设置，填写端口映射的信息(端口映射对外设置80或者8080是没有用的，尝试一下就知道了)，IP地址就填写路由器的地址，光猫也设置完成(如果以后要添加新的端口可以在这里设置)
![光猫路由1.png](resources\光猫路由1.png)
![光猫路由2.png](resources\光猫路由2.png)

### 检测公网是否可用
3. 两边都设置完，可以利用上面获取到的公网IP地址测试下：
    (1). 在光猫配置页面，把内网80端口映射到外部端口8001端口
    ![验证公网2.png](resources\验证公网2.png)
    (2). 使用你熟悉的后端语言写个服务接口，服务端口=80
    (3). 手机网络、或者使用其他网络访问:{公网IP地址}:{外部端口}/{接口地址}
    (4). 访问到数据即完成配置

## 利用阿里ddns实现ip自动解析到域名

### 说明一下，做定时域名绑定的原因和要点：
1. (绑定域名)：固定的域名比可变的IP容易管理
2. (定时)：绑定域名也只是大概20小时以内绑定一个IP，IP切换了就需要重新绑定
3. 只要调用ddns的频率远大于IP变动的频率，就基本不会丢失域名的绑定了，所以需要保证定时任务的存活

### 定时绑定域名需要：
0. 需要在阿里云申请的域名，然后到账号安全设置里取得**AccessKey**（*建议使用子账号分权*）:
    * 包含**AccessKey ID**和**AccessKey Secret**，**地域ID**需要自行查询

1. 官方有Java的实例代码：[实现动态域名解析DDNS](https://help.aliyun.com/document_detail/141482.html?spm=5176.11065259.1996646101.searchclickresult.46fd2881SgUCqH)
    * 官方使用的`https://jsonip.com/`可能会不稳定，替换为`https://api.ipify.org/`

2. 实现的方法很多，因为不是很重要的代码，所以删掉了，举个两个例子：
    * 方案1. 普通的java程序(直接服务上面文档就行)，一个main方法，执行完就结束=>使用Linux自带的crontab实现定时执行（往下看有例子可以参考）
    * 方案2. 使用Spring Task执行定时任务

3. Linux方面如何部署jdk不做介绍，ARM/X86都是一样的，唯一要注意的是，树莓派和部分手机等ARM性能比较差，方案2长时间运行JVM可能会有点压力，需要做一定处理：
    * 定时任务重启设备:
    ```bash
        配置crontab
        sudo crontab -e
        
        设置凌晨5点重启设备
        0 5 * * * sudo -u root reboot

        重启设备
        sudo reboot
    ```
    * 开机启动服务
    ```bash
        打开启动配置文件
        sudo vim /etc/rc.local
        最后一行加上:
        /jdk/jdk1.8/bin/java -jar /home/pi/ddns-task.jar > /home/pi/ddns-task.log 2>&1 &
    ```
    * 这里解释一下**rc.local** 为什么这样写：
        * `/jdk/jdk1.8/bin/java` rc.local相当早启动，配置好的java指令还没读取到配置，只能写全目录了 -- 实在不懂可以理解成桌面还没加载，所以读取不到桌面的快捷方式，你只能进去磁盘里找到启动程序运行。
        * `-jar` 这个跳过
        * `/home/pi/ddns-task.jar` 这就是你Spring Task程序打好的jar包
        * `> /home/pi/ddns-task.log 2>&1 &` 即是输出日志到`/home/pi/ddns-task.log`