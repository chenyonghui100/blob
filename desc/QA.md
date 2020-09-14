## 语法篇
---

#### <div id="foreach中使用&的问题"> foreach中使用&的问题</div>

###### 问题描述：
```php
$arr = [111, 222, 333, 444];
foreach ( $arr as &$value ) {
    //逻辑代码
}
var_dump($arr);
foreach ( $arr as $value ) {
    //逻辑代码
} 
var_dump($arr);

运行结果：
array(4) { [0]=> int(111) [1]=> int(222) [2]=> int(333) [3]=> &int(444) } 
array(4) { [0]=> int(111) [1]=> int(222) [2]=> int(333) [3]=> &int(333) }
```
>出现这种情况是因为在第一个foreach中，每次的循环都相当于：
>
>$value = &$arr[$i]; // $i 是$arr的索引
第一个foreach完成后，$value并没有注销掉，到第二个foreach时，每次的循环都相当于：
$value = $arr[$i]; // $i 是$arr的索引
但$value在第一个foreach中被定义为了一个引用值$value = &$arr[2]，所以第二个foreach会更新$arr[2]的值。

所以，再次使用$value前需要 unset($value);

**结论：在foreach中使用&时，循环完成后及时unset；以免后面使用相同变量时出现问题**

#### <div id="file_get_content"> file_get_content函数读取大文件时的问题</div>

#### <div id="str转int时超过最大值问题"> str转int时超过最大值问题</div>

#### <div id="file_get_content"> file_get_content函数读取大文件时的问题</div>



​	