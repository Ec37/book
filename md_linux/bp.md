# linux关于bashrc与profile的区别

## bashrc与profile的区别

* 要搞清`bashrc`与`profile`的区别，首先要弄明白什么是交互式`shell`和非交互式`shell`，什么是`login shell` 和`non-login shell`。

* 交互式模式就是`shell`等待你的输入，并且执行你提交的命令。这种模式被称作交互式是因为`shell`与用户进行交互。这种模式也是大多数用户非常熟悉的：登录、执行一些命令、签退。当你签退后，`shell`也终止了。 `shell`也可以运行在另外一种模式：非交互式模式。在这种模式下，shell不与你进行交互，而是读取存放在文件中的命令,并且执行它们。当它读到文件的结尾，shell也就终止了。

* `bashrc`与`profile`都用于保存用户的环境信息，`bashrc`用于交互式`non-loginshell`，而`profile`用于交互式`login shell`。系统中存在许多`bashrc`和`profile`文件，下面逐一介绍：

  1. `/etc/pro`此文件为系统的每个用户设置环境信息,当第一个用户登录时,该文件被执行.

  2. 并从`/etc/profile.d`目录的配置文件中搜集shell的设置.

  3. `/etc/bashrc`:为每一个运行`bash shell`的用户执行此文件.当`bash shell`被打开时,该文件被读取。有些`linux`版本中的`/etc`目录下已经没有了`bashrc`文件。

  4. `~/.pro`每个用户都可使用该文件输入专用于自己使用的`shell`信息,当用户登录时,该

  5. 文件仅仅执行一次!默认情况下,它设置一些环境变量,然后执行用户的`.bashrc`文件.

  6. `~/.bashrc`:该文件包含专用于某个用户的`bash shell`的`bash`信息,当该用户登录时以及每次打开新的`shell`时,该文件被读取.

  7. 另外,`/etc/profile`中设定的变量(全局)的可以作用于任何用户,而`~/.bashrc`等中设定的变量(局部)只能继承`/etc/profile`中的变量,他们是"父子"关系.

## 总结

* `/etc/profile`，`/etc/bashrc` 是系统全局环境变量设定
* `~/.profile`，`~/.bashrc`用户家目录下的私有环境变量设定
* 当登入系统时候获得一个shell进程时，其读取环境设定档有三步：
  
  1. 首先读入的是全局环境变量设定档`/etc/profile`，然后根据其内容读取额外的设定的文档，如：`/etc/profile.d和/etc/inputrc`

  2. 然后根据不同使用者帐号，去其家目录读取`~/.bash_profile`，如果这读取不了就读取`~/.bash_login`，这个也读取不了才会读取`~/.profile`，这三个文档设定基本上是一样的，读取有优先关系

  3. 然后在根据用户帐号读取`~/.bashrc`至于`~/.profile`与`~/.bashrc`的不区别都具有个性化定制功能`~/.profile`可以设定本用户专有的路径，环境变量，等，它只能登入的时候执行一次`~/.bashrc`也是某用户专有设定文档，可以设定路径，命令别名，每次`shell script`的执行都会使用它一次
