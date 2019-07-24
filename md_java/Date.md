# 日期时间相关
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