1、指出echo()、print()和print_r() 之间的区别

 echo 是PHP语句
 print()和print_r() 是函数，语句没有返回值，函数可以有返回值（即便没有用）

2、如何实现中文字符串的无乱码截取？

$str ="PHP测试例子";
$m_sub =mb_substr($str,0,4,"UTF-8");
echo $m_sub."<br>";
//PHP测试
3、编写代码，使得通过PHP获取前一天的时间，格式为2019-05-25 12:00:00

echo date('Y-m-d H:i:s',strtotime('-1 day')).'</br>';

$yesteday =time()-(24*60*60);
echo date('Y-m-d H:i:s',$yesteday)."<br>";
4、如何实现字符串的翻转功能？

$str ="abcdefg";
function strrevs($str){
	$len =strlen($str);
	$newstr='';
	for ($i=$len;$i>=0;$i--){

        $newstr .=$str{$i};
    }
    return $newstr;
}
echo strrevs($str)."<br>";
echo strrev("LOVE")."<br>";
5、用最简短的代码编写一个获取3个数字中最大值的函数

echo max(30,5,25)."<br>";
6、如何将字符09转换为十进制数字？

echo octdec('09')."<br>";
7、如何将1234567890转换成1,234,456,890每三位用逗号隔开的形式？

echo number_format('123456789')."<br>";
8、写一个函数，尽可能高效地实现从一个标准URL中取出文件的扩展名

$path ="http://www.sina.com.cn/abc/de/fg.php?id=2";
function msubstr($path){
	return substr(basename($path),0,strripos(basename($path),"?"));
}
echo msubstr($path);
9、有一数组 $a=array(8,2,7,0,5,1),请将其重新排序，按从小到大的顺序输出

sort()函数 对数字索引数组进行排序，然后讲过数组元素转换为字符串进行输出

$a=array(8,2,7,5,1);
sort($a);
print implode(" ",$a);
10、如何完成对SESSION过期时间的设置？

$time =1*60;
session_set_Cookie_params($time);
session_start();


 