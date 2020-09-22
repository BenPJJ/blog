# js位运算

![js位运算](img\js位运算.png)

按位与（&）、按位或（|）、按位非（~）、按位异或（^）、有符号左移（<<）、有符号右移（>>）、无符号右移（>>>）

## `<<`、`>>`、`>>>`三个运算符

### `<<`

``` js
var a = 1;
var b = 1 << 1;
var c = 1 << 2;
var d = 1 << 3;
console.log(a, a.toString(2).padStart(4, '0')) // 1 "0001"
console.log(b, b.toString(2).padStart(4, '0')) // 2 "0010" （1 * 2^1） 
console.log(c, c.toString(2).padStart(4, '0')) // 4 "0100" （1 * 2^2） 
console.log(d, d.toString(2).padStart(4, '0')) // 8 "1000" （1 * 2^3） 
```

`<<` 运算符实际就是将二进制得符号向左移动，并且用0去填充，即`左边数字 * 2 ^ 右边数字`

### `>>`

``` js
var a = 10;
var b = 10 >> 1;
var c = 10 >> 2;
var d = 10 >> 3;
console.log(a, a.toString(2).padStart(4, '0')) // 10 "1010"
console.log(b, b.toString(2).padStart(4, '0')) // 5 "0101" （1 * 2^1） 
console.log(c, c.toString(2).padStart(4, '0')) // 2 "0010" （1 * 2^2） 
console.log(d, d.toString(2).padStart(4, '0')) // 1 "0001" （1 * 2^3） 

var a = -10;
var b = -10 >> 1;
var c = -10 >> 2;
var d = -10 >> 3;
console.log(a, a.toString(2).padStart(4, '0')) // -10 "-1010"
console.log(b, b.toString(2).padStart(4, '0')) // -5 "-101"
console.log(c, c.toString(2).padStart(4, '0')) // -3 "0-11"
console.log(d, d.toString(2).padStart(4, '0')) // -2 "0-10"
```

`>>` 运算符实际就是将二进制得符号向右移动，即开平方，并向下取整。但是要注意如果前面得数字是负数的话，虽然也是开平方，但是它也是向下取整的，也就是说绝对值是会偏大的。

## `&`、`|` 两个运算符

``` js
var a = 9;
var b = 1 << 1;
var c = 1 << 2;
var d = 1 << 3;
console.log(a, a.toString(2).padStart(4, '0')) // 9 "1001"
console.log(b, b.toString(2).padStart(4, '0')) // 2 "0010" （1 * 2^1） 
console.log(c, c.toString(2).padStart(4, '0')) // 4 "0100" （1 * 2^2） 
console.log(d, d.toString(2).padStart(4, '0')) // 8 "1000" （1 * 2^3） 

var e = a|b;
console.log(e, e.toString(2).padStart(4, '0')) // 11 "1011"
var f = a&d;
console.log(e, e.toString(2).padStart(4, '0')) // 8 "1000"
```

可以看出，`|` 运算符的作用是对比二进制时，如果有一位为1，那就结果为1；`&` 则是必须都为1则为1，反之为0

## `~` 运算符

``` js
var a = 1; // 二进制 00000000000000000000000000000001
var b = ~a; // 二进制 11111111111111111111111111111110
console.log(a, a.toString(2).padStart(4, '0')) // 1 "0001"
console.log(b, b.toString(2).padStart(4, '0')) // -2 "0-10"
```

js中的数字默认是有符号的。有符号的32位二进制的最高位也就是第一位数字代表着正负，1代表负数，0代表整数。那到底`11111111111111111111111111111110`等于多少呢？最高位为1代表负数，负数的二进制转化为十进制：符号位不变，其他位取反加1，取反之后为10000000000000000000000000000001，加一之后为10000000000000000000000000000010，十进制为-2

## 位运算应用

### 判断奇偶

前端经常会有列表展示，隔一行一个效果。这种就需要判断奇偶了。这种代码的原理是将二进制数字前面所有的位数全部清零，只需要判断最后一位数字是1还是0就可以判断奇偶了

``` js
function test(num) {
  return !!(num&1); // true为奇数，false为偶数
} 
```



