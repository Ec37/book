# linux日志查看

## tail、head、cat、tac、sed、less、echo

1. `tail [必要参数] [选择参数] [文件]`

    -f 循环
    -q 不显示处理信息
    -v 显示详细的处理信息
    -c<数目> 显示的字节数
    -n<行数> 显示的行数
    -q,--quiet,--slient 当有多个文件参数时，不输出各个文件名
    -s,--sleep-interval=5 与-f合并，表示在每次反复的间隔休眠5秒
    `tail -n 100 catalina.out //查询日志尾部最后的100行日志内容`
    `tail -n +100 catalina.out //查询100行之后的内容`
    `tail -fn 100 catalina.out //循环实时查询最后100行的内容(最常用) `

2. `head`
    `head -n 1000 catalina.out //查询日志文件头10行`
    `head -n -1000 catalina.out //查询日志文件除了最后10行的其他所有日志`
    -其他参数与tail类似

3. `cat`
    cat是将文件第一行到最后一行连续打印出来
    `cat catalina.out //一次显示整个文件`
    `cat > catalina.out.n //创建一个新文件`
    `cat file1.t file2.t > file.t //将几个文件合并成一个新文件，不能已有编辑`
    `cat -n log.1 > log.2 //将一个日志文件的内容追加到另一个`
    `cat : > log.0 //清空一个日志文件`
    `>的意思是创建，>>的意思是追加`
    -其他参数和tail类似

4. `tac`
    tac就是将最后一行到第一行反向在屏幕输出出来

5. `sed`
    这个命令可以查找日志文件特定的一段，也可以根据时间的一个范围查找
    `sed -n '2,100p' catalina.out  //按照行号`
    `sed -n '/2019-11-01 00:00:00/,/2019-12-30 23:59:59/p' catalina.out //按照时间段`

6. `less`
    `less catalina.out`
    说明:shift+G到文件最后一行 输入?加上你要搜索的关键字 例如?hello回车后可以用shift+n在关键字间切换

7. `echo`
    `echo "echotext"`
