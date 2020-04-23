1、include 和 require 都能把另外一个文件包含到当前文件中 他们有什么区别?include 和 include_once 又有什么区别?

二者区别只有一个，那就是对包含文件的需求程度

include 就是包含，如果被包含的文件不存在的话， 那么则会提示一个错误，但是程序会继续执行下去。

require 意思是需要，如果被包含文件不存在或者 无法打开的时候，则会提示错误，并且会终止程序的执行。

这两种结构除了在如何处理失败之外完全一样。

once 的意思是一次，那么 include_once 和 require_once 表示只包含一次，避免重复包含。

 

2、用最少的代码写一个求 3 值最大的函数

 ![img](https://images2018.cnblogs.com/blog/1128628/201802/1128628-20180228223717197-491717760.png)

 

3、表单中 get 与 post 提交方法的区别?

3.1、GET 请求能够被 cache，GET 请求能够被保存在浏览器的浏览历史 里面(密码等重要数据 GET 提交，别人查看历史记录，就可以直接看 到这些私密数据)POST 不进行缓存。

3.2、GET 参数是带在 URL 后面，传统 IE 中 URL 的最大可用长度为 2053 字符，其他浏览器对 URL 长度限制实现上有所不同。POST 请求无长 度限制(目前理论上是这样的)。

3.3、GET 提交的数据大小，不同浏览器的限制不同，一般在 2k-8K 之间， POST 提交数据比较大，大小靠服务器的设定值限制，而且某些数据 只能用 POST 方法「携带」，比如 file。

3.4、全部用 POST 不是十分合理，最好先把请求按功能和场景分下类， 对数据请求频繁，数据不敏感且数据量在普通浏览器最小限定的 2k 范围内，这样的情况使用 GET。其他地方使用 POST。

3.5、GET 的本质是「得」，而 POST 的本质是「给」。而且，GET 是「幂 等」的，在这一点上，GET 被认为是「安全的」。但实际上 server 端 也可以用作资源更新，但是这种用法违反了约定，容易造成 CSRF(跨 站请求伪造)。

 

4、用 PHP 打印出前一天的时间

格式是 2005-5-10 22:21:21

```
echo date('Y-m-d H:i:s',time()-24*3600);
或
echo date('Y-m-d H:i:s',strtotime('-1 day'));
```

 

5、假设现在有一个字符串 ww.baidu.com 如何使用 PHP 对他进行操作使字符串以 moc.udiab.输出?

```
$str``=``'www.baidu.com'``;``//先替换，再反转``echo` `strrev``(``'www'``,``''``,``$str``);
```

　　

6、用 php 写出显示客户端 IP 与服务器 IP 的代码

客户端 IP:

```
   $SERVER[“REMOTE_ADDR”]
```

或者

```
   getenv('REMOTE_ADDR');
```

服务器 IP: $_SERVER[“SERVER_ADDR”]

 

 

7、写个函数用来对二维数组排序

 ![img](https://images2018.cnblogs.com/blog/1128628/201802/1128628-20180228225755008-178722459.png)

 

 8、`'01' == '1';` 结果是 TRUE

```php
in_array('01',array('1'))；结果是1
```

 ![img](https://images2018.cnblogs.com/blog/1128628/201802/1128628-20180228230702385-1004483674.png)

 

 

9、简述单引号和双引号的用法 双引号串中的内容可以被解释而且替换，

单引号串中的内容总被认为是普通字符。

 

10、计算某段字符串中某个字符出现的次数

 (例如:gdfgfdgd59gmkblg 中 g 的次数) $text = 'gdfgfdgd59gmkblg';

```
echo substr_count ( $text,'g');
 
```

 

11、有一个楼梯n级台阶,每次可以上一级或两级台阶,有几种不同上法?

 这是一个经典的递归问题.也就是费波纳西级数.
f(n) = f(n-1) + f(n-2).
如果我们第一部选1个台阶,那么后面就会剩下n-1个台阶,也就是会有f(n-1)种走法.如果我们第一部选2个台阶,后面会有f(n-2)个台阶.因此,对于n个台阶来说,就会有f(n-1) + f(n-2)种走法.
因此,1个台阶f(1) = 1.
f(2) = 2,
f(3) = 3 
f(4) = 5 
f(5) = 8 
f(6) = 13 
f(7) = 21 
f(8) = 34 
f(9) = 55 
f(10) = 89 
f(11) = 89+55 = 144 
f(12) = 144 + 89 = 233
.
2.
这类题可这样理解 
假设走到第n阶有f(n)种走法,走到第n+1阶有f(n+1)种走法; 
则走到第n+2阶,则可分成两种情况:
一,最后一步是从第n阶直接登两级到第n+2阶 
二,最后一步是从第n+1阶直接登一级到第n+2阶 
由于从地面到第n阶,和到第n+1阶的走法已经知道 
故从地面到第n+2阶的走法:
f(n+2)=f(n)+f(n+1) 
n=1时,1种走法 
n=2时,2种走法 
n=3时,1+2=3种走法 
n=4时,2+3=5种走法 

 

 

12、普通传值与引用传值及unset

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
<?php
//普通传值
$param1=1; 
$param2=2; 
$param2 = $param1; 
$param1 = 5; //变量1和变量2是两块内存,互不影响;
echo $param2; //所以此处还是显示为1

//引用传值 ↓↓
$param1=1; 
$param2=2; 
$param2 = &$param1; //把变量1的内存地址赋给变量2;此时的变量2和变量1全等;
echo $param2;// 1
$param1 = 5; //变量1和变量2是一处内存,改变其中一个,另外一个也被改变;
echo $param2; //显示为5
?>


$a = 1;
$b = &$a;
unset($a);
echo $b; //1
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

首先,要理解变量名存储在内存栈中,它是指向堆中具体内存的地址,通过变量名查找堆中的内存;
普通传值,传值以后,是不同的地址名称,指向不同的内存实体;
引用传值,传引用后,是不同的地址名称,但都指向同一个内存实体;改变其中一个,另外一个就也被改变;

unset并没有真正销毁变量的作用...仅仅是切断了变量与内存之间的关系，内存只要还被引用着就不会被释放; $b和$a同时指向1,切断其中$a的关系,$b还是指向1,所以上题不报错,照样输出1。

 

13、

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
//--------------如何理解static静态变量-----------
 
/** 普通局部变量 */
function local() {
    $loc = 0; //这样，如果直接不给初值0是错误的。
    ++$loc;
    echo $loc . '<br>';
}
local(); //1
local(); //1
local(); //1
echo '===================================<br/>';
 
/** static静态局部变量 */
function static_local() {
    static $local = 0 ; //此处可以不赋0值
    $local++;
    echo $local . '<br>';
}
static_local(); //1
static_local(); //2
static_local(); //3
//echo $local; 注意虽然静态变量，但是它仍然是局部的，在外不能直接访问的。
echo '=======================================<br>';
 
/** static静态全局变量(实际上:全局变量本身就是静态存储方式,所有的全局变量都是静态变量) */
function static_global() {
    global $glo; //此处，可以不赋值0，当然赋值0，后每次调用时其值都为0，每次调用函数得到的值都会是1，但是不能想当然的写上"static"加以修饰，那样是错误的.
    $glo++;
    echo $glo . '<br>';
}
static_global(); //1
static_global(); //2
static_global(); //3
?>
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

在 PHP 中，作用域是不重叠的，函数之外的是全局变量，

函数内部定义的则是局部变量，二者是两个不同的变量，除非 在函数内使用 global 显式声明使用全局变量或直接用 $_GLOBALS 来引用。

 

 14、$arr = array(‘james’, ‘tom’, ‘symfony’); 请将$arr 数组的值用’ , ’分割并合并成字符串输出

echo implode(‘ , ’ , $arr);

$str = ‘jack, james, tom, symfony’;请将$str 用’ , ’分割,并把分割后的值放到$arr 数组中

$arr = explode(‘ , ’ , $str);

 

15、说出数组涉及到的常用函数

array-- 声明一个数组
count -- 计算数组中的单元数目或对象中的属性个数

foreach-- 遍历数组

list -- 遍历数组

explode-- 将字符串转成数组
implode-- 将数组转成一个新字符串
array_merge-- 合并一个或多个数组
is_array-- 检查是否是数组
print_r -- 输出数组
sort -- 数组排序
array_keys-- 返回数组中所有的键名

array_values-- 返回数组中所有的值
key-- 从关联数组中取得键名

 

 16、字符串的常用函数

trim()-- 去除字符串首尾处的空白字符(或者其他字符)

strlen()-- 字符串长度
substr()-- 截取字符串
str_replace()-- 替换字符串函数

substr_replace()-- 对指定字符串中的部分字符串进行替换 

strstr()-- 检索字符串函数

explode()-- 分割字符串函数

implode()-- 将数组合并成字符串

str_repeat()-- 重复一个字符串

addslashes()-- 转义字符串

htmlspecialchars()--THML 实体转义

 

17、写一个函数,能够遍历一个文件夹下的所有文件和子文件夹

 ![img](https://images2018.cnblogs.com/blog/1128628/201802/1128628-20180228235340027-165321536.png)

 

18、以下代码的执行后是,$result 值为: ![img](https://images2018.cnblogs.com/blog/1128628/201802/1128628-20180228235719042-883650288.png)

答案：false

is_null-- 检测变量是否为NULL，
如果变量是 null 则返回 TRUE，否则返回 FALSE。

在下列情况下一个变量被认为是 NULL: 1) 被赋值为 NULL
2) 尚未被赋值
3) 被 unset()

 

19、请列举出你所知道的全局环境变量

 $_ENV;

$_SERVER;

$_REQUEST

$_FILES

$_SESSION;

$_COOKIE;

$_GET;

$_POST;

$GLOBALS;

 

20、session 与 cookie 的区别?

session:储存用户访问的全局唯一变量,存储在服务器上的 php 指 定的目录中的(session_dir)的位置进行的存放

cookie:用来存储连续访问一个页面时所使用，是存储在客户端， 对于 Cookie 来说是存储在用户 WIN 的 Temp 目录中的。

两者都可通过时间来设置时间长短