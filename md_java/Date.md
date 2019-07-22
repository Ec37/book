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


    >SimpleDateFormat函数语法：
    G 年代标志符
    y 年
    M 月
    d 日
    h 时 在上午或下午 (1~12)
    H 时 在一天中 (0~23)
    m 分
    s 秒
    S 毫秒
    E 星期
    D 一年中的第几天
    F 一月中第几个星期几
    w 一年中第几个星期
    W 一月中第几个星期
    a 上午 / 下午 标记符 
    k 时 在一天中 (1~24)
    K 时 在上午或下午 (0~11)
    z 时区

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

2. __区间天数：__
```java 
    import java.text.ParseException;
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    import java.util.Date;

    /**
    *      实现1949-10-1  ---  2016-8-15 之间的天数。
    *      方法一：
    *      通过Calendar类的日期比较
    *          1，日期是跨年份的
    *          2，年份有闰年和平年
    *      思路：
    *          1，通过SimpleDateFormat初始化时间时刻
    *          2，Date对象的方法大多过时，我们用Calendar类来计算
    *          3，Calendar中的get方法可以获取各个字段的值，例如：DAY_OF_YEAR 一年里当前年时刻的天数
    *          4，计算两个年份之间相差多少年
    *          5，判断平年还是闰年 平年加366天  闰年加365天
    *          6，年份的天数加上当前年时刻天数的差得到结果。
    *
    *      方法二：
    *      Date类的gettime方法返回当前对象一个long值 （单位毫秒）
    *      思路：
    *          1，分别计算两个对象的long值。
    *          2，再用long值想减。
    *          3，用相减的毫秒换算成天数。
    *
    */

    public class DateTest {
        public static void main(String[] args) {
            String dateStr1 = "1949-10-01";
            String dateStr2 = "2016-08-15";
            SimpleDateFormat format1 = new SimpleDateFormat("yyyy-MM-dd");
            SimpleDateFormat format2 = new SimpleDateFormat("yyyy-MM-dd");
            try {
                Date date1 = format1.parse(dateStr1);
                Date date2 = format2.parse(dateStr2);

                System.out.println("1949年10月1日和2016年8月15日相差了："+differentDays(date1,date2)+"天！");
            System.out.println(differentDayMillisecond(date1,date2));
            } catch (ParseException e) {
                e.printStackTrace();
            }
        }
        public static int differentDays(Date date1,Date date2){
            Calendar calendar1 = Calendar.getInstance();
            calendar1.setTime(date1);
            Calendar calendar2 = Calendar.getInstance();
            calendar2.setTime(date2);

            int day1 = calendar1.get(Calendar.DAY_OF_YEAR);
            //System.out.println(day1);
            int day2 = calendar2.get(Calendar.DAY_OF_YEAR);
            //System.out.println(day2);
            int year1 = calendar1.get(Calendar.YEAR);
            int year2 = calendar2.get(Calendar.YEAR);

            if (year1 != year2)  //不同年
            {
                int timeDistance = 0;
                for (int i = year1 ; i < year2 ;i++){ //闰年
                    if (i%4==0 && i%100!=0||i%400==0){
                        timeDistance += 366;
                    }else { // 不是闰年
                        timeDistance += 365;
                    }
                }
                return  timeDistance + (day2-day1);
            }else{// 同年
                return day2-day1;
            }

        }

        public  static int differentDayMillisecond (Date date1,Date date2)
        {


            int day = (int)((date2.getTime()-date1.getTime())/(3600*1000*24));
            return day;
        }
    }
```