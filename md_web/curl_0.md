# cUrl入门笔记

* 声明：本文主要搬运自阮一峰的博文

## 常见用法

* 查看网页源码
  
```bash
    curl www.baidu.com
```

* `-o` 要把网页保存下载，可以使用-o参数

```bash
    curl -o [文件名] www.baidu.com
```

* `-L` 可以实现自动跳转

```bash
    curl -L www.baidu.com
```

* `-i` 显示Http Response头信息，同时也会返回页面内容的源代码

```bash
    curl -i www.baidu.com
```

* `-I` 只显示Http Response头信息，不会返回页面内容

```bash
    curl -I www.baidu.com
```

* `-v` 显示通信过程，可以显示一次http通信的整个过程，包括端口连接和http request头信息

```bash
    curl -v www.baidu.com
```

* `--trace` 如果上面信息不够，可以用--trace查看更详细的通信过程

```bash
    curl --trace test.txt www.baidu.com
    或者
    curl --trace-ascii test.txt www.baidu.com
    执行后，打开test.txt查看
```

* 发送Get表单信息

```bash
    curl www.baidu.com/s?ie=UTF-8&wd=阮一峰
```

* `-X POST`发送Posh表单信息，需要用到-data参数，网址和数据要分开

```bash
    curl -X POST --data "key=value" www.baidu.com/form.action
```

* `-X` http的动词

```bash
    curl -X POST www.baidu.com
    curl -X DELETE www.baidu.com
```

* `--form` 文件(表单)上传

```html
    如果文件上传表单是这样子的:
    <form method="POST" enctype='multipart/form-data' action="upload.action">
      <input type="file" name="upload">
      <input type="submit" name="subBtn" value="OK">
    </form>
```

```bash
    curl --form upload=@localfilename --form subBtn=OK [URL]
```

* `--referer` 参数 Referer字段，声明当前请求来自哪里

```bash
    在http request头信息中，增加一个referer字段，表示你是从哪里过来的。
    //从google到baidu
    curl --referer http://www.google.com http://www.baidu.com
```

* `--user-agent` 参数 User Agent字段

```bash
    这个字段用来表示客户端设备的信息。

    curl --user-agent “[User Agent]" [URL]
```

* `--cookie`参数，可以让curl发送cookie

```bash
    curl --cookie "name=xxx" www.baidu.com

    至于具体的cookie设置，可以从http response头信息中的Set-Cookie字段中得到。

    -c cookie-file可以保存服务器返回的cookie到文件，

    -b cookie-file可以使用这个文件作为cookie信息，作为后续的请求。

    curl -c filename http://www.baidu.com
    curl -b filename http://www.baidu.com
```

* `--header` 自行增加http request头信息

```bash
    curl --header "Content-Type:application/json" http://www.baidu.com
```

* `--user` 有些网站需要http认证，这里需要用到`--user`参数

```bash
    curl --user name:password www.baidu.com
```
