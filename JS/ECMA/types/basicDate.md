# javascript中关于日期和时间的基础知识

&emsp;&emsp;在介绍Date对象之前，首先要先了解关于日期和时间的一些知识。比如，闰年、UTC等等。深入了解这些，有助于更好地理解javascript中的Date对象。本文将介绍javascript关于日期和时间的基础知识

&nbsp;

### 标准时间

&emsp;&emsp;一般而言的标准时间是指GMT和UTC，以前是GMT，现在是UTC

**GMT**

&emsp;&emsp;格林尼治标准时间(GMT)是指位于伦敦郊区的皇家格林尼治天文台的标准时间，因为本初子午线被定义在通过那里的经线

&emsp;&emsp;理论上来说，格林尼治标准时间的正午是指当太阳横穿格林尼治子午线时(也就是在格林尼治上空最高点时)的时间。由于地球在它的椭圆轨道里的运动速度不均匀，这个时刻可能和实际的太阳时相差16分钟

&emsp;&emsp;地球每天的自转是有些不规则的，而且正在缓慢减速。所以，格林尼治时间已经不再被作为标准时间使用。现在的标准时间由世界协调时间(UTC)提供

**UTC**

&emsp;&emsp;世界协调时间(UTC)又称世界统一时间，世界标准时间，国际协调时间，全称Coordinated Universal Time，是以原子时秒长为基础，在时刻上尽量接近于世界时的一种时间计量系统&nbsp;

&emsp;&emsp;这套时间系统被应用于许多互联网和万维网的标准中，中国大陆、中国香港、中国澳门、中国台湾、蒙古国、新加坡、马来西亚、菲律宾、西澳大利亚州的时间与UTC的时差均为+8，也就是UTC+8

&emsp;&emsp;在军事中，协调世界时区会使用&ldquo;Z&rdquo;来表示。又由于Z在无线电联络中使用&ldquo;Zulu&rdquo;作代称，协调世界时也会被称为"Zulu time"

&nbsp;

### 日期时间字符串格式

&emsp;&emsp;ECMAScript定义了一个基于简化的ISO8601扩展格式的日期时间的字符串互换格式

&emsp;&emsp;日期时间完整格式为: &nbsp;YYYY-MM-DDTHH:mm:ss.sssZ

&emsp;&emsp;注意：前置0不能省略，否则在完整格式的情况下会报错

<div>
<pre>YYYY        公历中年的十进制数字，如果这个参数值在0-99之间，则向它加上1900
-           在字符串中直接以&ldquo;-&rdquo;(破折号)出现两次
MM          一年中的月份，从01(一月)到12(十二月)
DD          月份中的日期，从01到31
T           在字符串中直接以&ldquo;T&rdquo;出现，用来表明时间元素的开始
HH          用两个十进制数字表示的，自午夜0点以来的小时数
:           在字符串中直接以&ldquo;:&rdquo;(冒号)出现两次
mm          是用两个十进制数字表示的，自小时开始以来的分钟数
ss          是用两个十进制数字表示的，自分开始以来的秒数
.           在字符串中直接以&ldquo;.&rdquo;(点)出现
sss         是用三个十进制数字表示的，自秒开始以来的毫秒数
Z           是时区偏移量，由（&ldquo;Z&rdquo;(指UTC)或&ldquo;+&rdquo;或&ldquo;-&rdquo;）和后面跟着的时间表达式hh:mm组成</pre>
</div>

&emsp;&emsp;只表示日期的格式: &nbsp;YYYY YYYY-MM YYYY-MM-DD

&emsp;&emsp;注意：所有数字必须是10进制的。如果缺少MM或DD字段，用&ldquo;01&rdquo;作为它们的值。如果缺少mm或ss字段，用&ldquo;00&rdquo;作为它们的值，对于缺少的sss用&ldquo;000&rdquo;作为它的值。对于缺少的时区偏移量用&ldquo;Z&rdquo;

&nbsp;

### 闰年

&emsp;&emsp;年分为闰年和平年，平年有365天，闰年有366天，闰年的2月比平年多一天

&emsp;&emsp;闰年的定义是(可被4整除)且((不可被100整除)或(可被400整除))的年份

&emsp;&emsp;口诀是：四年一闰，百年不闰，四百年再闰

<div>
<pre>function IsLeapYear(year){
    if(typeof year == 'number'){
        if((year % 4 === 0 &amp;&amp; year % 100 !== 0)  || year % 400 === 0){
            return 'leap year'
        }else{
            return 'common year'
        }
    }
    return 'please input number'
}</pre>
</div>
<div>
<pre>console.log(IsLeapYear(4));//'leap year'
console.log(IsLeapYear(400));//'leap year'
console.log(IsLeapYear(2000));//'leap year'
console.log(IsLeapYear(1900));//'common year'</pre>
</div>

&nbsp;

### 月日

&emsp;&emsp;一年有12个月，其中4、6、9、11月每月有30天；如果是闰年，2月有29天，否则 ，2月有28天。1、3、5、7、8、10、12月每月有31天

&emsp;&emsp;在javascript中，月的计算从0开始，所以1-12月，分别用0-11来表示；而日的计算则从1开始，1就代表第1天，以此类推

<div>
<pre>if(month == 2){
    //如果是闰年
    if((year % 4 === 0 &amp;&amp; year % 100 !== 0)  || year % 400 === 0){
        days = 29;
    //如果是平年
    }else{
        days = 28;
    }
//如果是第4、6、9、11月
}else if(month == 4 || month == 6 ||month == 9 ||month == 11){
    days = 30;
}else{
    days = 31;
}</pre>
</div>

&emsp;&emsp;在javascript中，月份的简写经常在日期字符串中使用

<div>
<pre>一月       Jan January
二月       Feb February
三月       Mar March
四月       Apr April
五月       May May
六月       Jun June
七月       Jul July
八月       Aug August
九月       Sep September
十月       Oct October
十一月     Nov November
十二月     Dec December</pre>
</div>

&nbsp;

### 星期

&emsp;&emsp;星期是从星期日开始，到星期六结束，分别用0-6来表示

&emsp;&emsp;在javascript中，各星期的简写经常在日期字符串中使用

<div>
<pre>星期日    sunday         Sun
星期一    monday         Mon
星期二    Tuesday        Tue
星期三    Wednesday      Wed
星期四    Thursday       Thu
星期五    Friday        Fri
星期六    Saturday       Sar</pre>
</div>

&nbsp;

### 时分秒

<div>
<pre>    1天 = 24小时 = 24*60(1440)分 = 24*60*60(86400)秒 = 86,400,000毫秒
    1分= 60秒
    1小时 = 3600秒
    1天 = 86400秒</pre>
</div>

&emsp;&emsp;Date对象返回的是一个毫秒数，经常需要将其换算成时分秒的形式

<div>
<pre>date = 100000s
day(天) = Math.floor(100000/86400) = 1
hour(小时) = Math.floor((100000%86400)/3600) = 3
minute(分) = Math.floor((100000%3600)/60) = 46
second(秒) = Math.floor(100000%60)=40
console.log(100000 === 1*86400+ 3*3600+ 46*60+40);//true</pre>
</div>
