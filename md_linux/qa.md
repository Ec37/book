# linux常见问题解决方法

## ^M: bad interpreter: No such file or directory解决

问题: 执行sh文件时提示^M: bad interpreter: No such file or directory

原因：sh脚本在windows下用记事本编写的，不同系统引发了编码问题

验证：

  1. `vi test.sh`
  2. `:set ff`或者`:set fileformat`
  3. 可以看到`fileformat=dos`

修复：

  1. `vi test.sh`
  2. `:set ff=unix`或者`:set fileformat=unix`
  3. `:wq`保存退出
  