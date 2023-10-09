# 1. PHP解惑
## 1.1 empty,isset,is_null区别
1. `isset()`是用来判断变量是否设置了值，<mark style="background: #FFB86CA6;">只要不是NULL就会返回true</mark>
2. `empty()`是用来判断值是否为空，也就是说有如下情况时返回真值：变量是一个<mark style="background: #FFB86CA6;">空字符串，false，空数组，NULL，0，''，以及被unset删除后的变量。</mark>
3. `is_null()`函数用来判断变量内容是否是NULL值，即<mark style="background: #FFB86CA6;">返回真值的条件仅为变量是NULL时。</mark>
**正确检测一个变量**
```php
if(empty($var)) {
	// todo ...
} else {
	// todo ...
}
```
## 1.2 变量作用域
在PHP中定义一个变量后，在脚本任意位置都可以存取访问，这被称为“全局变量”，而定义在函数或类的方法中的变量只可以在函数内部访问，这叫作“局部变量”。
