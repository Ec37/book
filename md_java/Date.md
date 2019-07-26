# 时间的问题

## Date、String互转

1. __String转Date：__

      ```java
      String str = "2007-1-18";
      try {
          date = format1.parse(str);
          data = format2.parse(str);
        }catch(ParseException e) {
            e.printStackTrace();
        }
    ```

2. __Date转String：__

    ```java
    String str = null;
    date=new Date();
    DateFormat format1 = new SimpleDateFormat(“yyyy-MM-dd”);
    DateFormat format 2= new SimpleDateFormat(“yyyy年MM月dd日 HH时mm分ss秒”);
    str=format1.format(date);
    str=format2.format(date);
    ```

* SimpleDateFormat函数语法：
  * G 年代标志符
  * y 年
  * M 月
  * d 日
  * h 时 在上午或下午 (1~12)
  * H 时 在一天中 (0~23)
  * m 分
  * s 秒
  * S 毫秒
  * E 星期
  * D 一年中的第几天
  * F 一月中第几个星期几
  * w 一年中第几个星期
  * W 一月中第几个星期
  * a 上午 / 下午 标记符
  * k 时 在一天中 (1~24)
  * K 时 在上午或下午 (0~11)
  * z 时区

## 日期时间计算

1. __日期加减--Calendar：__

    ```java
    Date date = new Date();//获取当前时间
    Calendar calendar = Calendar.getInstance(); //创建Calendar 的实例
    calendar.set(Calendar.YEAR, -1);//当前时间减去一年，即一年前的时间
    calendar.set(Calendar.MONTH, -1);//当前时间减去一个月，即一个月前的时间
    calendar.set(Calendar.DAY_OF_MONTH,-1); //当前时间减去一天，即一天前的时间
    calendar.getTime();//返回当前时间的毫秒数
    ```

## System.nanoTime与System.currentTimeMillis的区别

java中产生随机数函数以及线程池中的一些函数使用的都是System.nanoTime

1. System.nanoTime提供相对精确的计时，但是不能用他来计算当前日期，在jdk中的说明如下：
    > 返回最准确的可用系统计时器的当前值，__以毫微秒为单位__。此方法只能用于测量已过的时间，与系统或钟表时间的其他任何时间概念无关。返回值表示从某一固定但任意的时间算起的毫微秒数（或许从以后算起，所以该值可能为负）。此方法提供毫微秒的精度，但不是必要的毫微秒的准确度。它对于值的更改频率没有作出保证。在取值范围大于约 292 年（263 毫微秒）的连续调用的不同点在于：由于数字溢出，将无法准确计算已过的时间

2. System.currentTimeMillis返回的是从1970.1.1 UTC 零点开始到现在的时间，__精确到毫秒__，平时我们可以根据System.currentTimeMillis来计算当前日期，星期几等，可以方便的与Date进行转换，下面是jdk中的介绍：
    > 返回以毫秒为单位的当前时间。注意，当返回值的时间单位是毫秒时，值的粒度取决于底层操作系统，并且粒度可能更大。例如，许多操作系统以几十毫秒为单位测量时间。请参阅 Date 类的描述，了解可能发生在“计算机时间”和协调世界时（UTC）之间的细微差异的讨论。
