## 算法篇

### <div id="二维数组中的查找"> 二维数组中的查找</div> 

#### 题目描述
在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

解题思路：
> 思路:
>
* 矩阵是有序的，从左下角来看，向上数字递减，向右数字递增，因此:
* 从左下角开始查找，当要查找数字比左下角数字大时。右移
* 要查找数字比左下角数字小时，上移

##### 代码实现：
```php
<?php

function Find($target, $array)
{
    // write code here
    
      $lon = count($array);//二维数组长度
       return seach2($lon-1,0,$array,$target);
}

function seach2($lon,$com,$array,$target){
    $comn = count($array[0]);//二维数组内数组长度
    if($lon<0 ||$com >= $comn){
        return false;
    }
    if($array[$lon][$com]<$target){
        return seach2($lon,$com+1,$array,$target);
    }elseif($array[$lon][$com]>$target){
        return seach2($lon-1,$com,$array,$target);
    }else{
        return true;
    }
}
```



### <div id="替换空格"> 替换空格</div> 

#### 题目描述
请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

解题思路：
> 思路:
>
* 使用php字符串转数组函数（explode('',$str)）将字符串按照空格拆分为数组
* 然后使用数组转字符串函数（implode('',$arr)）使用‘%20’连接起来

##### 代码实现：
```php
<?php
function replaceSpace($str)
{
    // write code here
    
    $arr = explode(' ',$str);
    $strs = implode('%20',$arr);
    return $strs;
}
```
### <div id="重建二叉树"> 重建二叉树</div> 
#### 题目描述
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。。

解题思路：
> 思路:
>
* 明白两点：1.前序遍历是根左右，中序遍历是左根右
* 2.使用递归来解决

##### 代码实现：
```php
<?php

class TreeNode{
    var $val;
    var $left = NULL;
    var $right = NULL;
    function __construct($val){
        $this->val = $val;
    }
}
function reConstructBinaryTree($pre, $vin)
{
    if($pre && $vin){
        $treeRoot = new TreeNode($pre[0]);
        $index = array_search($pre[0],$vin);
        $treeRoot->left = reConstructBinaryTree(array_slice($pre,1,$index),array_slice($vin,0,$index));
        $treeRoot->right = reConstructBinaryTree(array_slice($pre,$index+1),array_slice($vin,$index+1));
        return $treeRoot;
    }
 
}
```

解读：首先需要有一个节点类，用来实例化节点对象，二叉树的节点有三个属性，data，left，right。
函数：array_search($pre[0],$vin);返回数组中$pre[0]的下标。因为先序遍历的第一个数是根节点，所以中序遍历所对应的数字节点可以将原序列分为两部分（left和right）。

array_slice($arr,$start,$len) 

|:-:|:-:|
|$arr|必需。规定数组。|
|start|必需。数值。规定取出元素的开始位置。 0 = 第一个元素。|
|$len|可选。数值。规定被返回数组的长度。|

### <div id="反转链表"> 反转链表</div> 
#### 题目描述
输入一个链表，反转链表后，输出新链表的表头。

解题思路：
> 思路:
>
* 首先需要一个空节点，头指针的next要指向这个空节点(注意，这个时候原头结点的next需要用一个指针指到这个节点上，否则会丢失节点)。之后循环遍历，将节点逆置

##### 代码实现：

```php
<?php
/*class ListNode{
    var $val;
    var $next = NULL;
    function __construct($x){
        $this->val = $x;
    }
}*/
function ReverseList($pHead)
{
    // write code here
     $pre = null;
    while($pHead != null){
        $tmp = $pHead->next;      
        $pHead->next = $pre;
        $pre = $pHead;
        $pHead = $tmp;
    }
    return $pre;
}
```
>最后$pHead指在空节点上，$pre指在最后一个非空节点上，所以应该return $pre;




​	
