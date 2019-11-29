# canvas画图出现模糊现象

使用canvas 进行画图在分辨率高的设备上会出现模糊现象

## 解决思路

### 一：改变canvas渲染的像素

**情况：**画1像素的线条看起来模糊不清，好像更宽的样子

​	canvas 的每条线都有一条无限细的“中线”，线条的宽度是从中线向两侧延伸的。如果还是从第2个像素点画一条线，那么线条得中线就会靠齐到第2个像素得起点，但是计算机不允许出现<1px 的图形，所以会做个折中，把两个像素都绘制，这样一来，本来1px 的线条，就成了看起来2px 宽的线条

**解决：**把线条中线和像素中间点对齐

``` js
context.translate(0.5, 0.5);
```

### 二：设置显示比例

 在浏览器的window变量中有一个devicePixelRatio的属性，该属性决定了浏览器会用几个（通常是2个）像素点来渲染1个像素 ， 举例来说，假设某个屏幕的devicePixelRatio的值为2，一张100x100像素大小的图片，在此屏幕下，会用2个像素点的宽度去渲染图片的1个像素点，因此该图片在此屏幕上实际会占据200x200像素的空间，相当于图片被放大了一倍，因此图片会变得模糊。 

**解决：** 创建一个两倍于实际大小的canvas，然后用css样式把canvas限定在实际的大小

## 基本配置

``` js
const devicePixelRatio = window.devicePixelRatio || 1;
const backingStoreRatio = context.webkitBackingStorePixelRatio ||
      context.mozBackingStorePixelRatio ||
      context.msBackingStorePixelRatio ||
      context.oBackingStorePixelRatio ||
      context.backingStorePixelRatio || 1;
const ratio = devicePixelRatio / backingStoreRatio;
canvas.width = this.width * ratio;
canvas.height = this.height * ratio;
context.scale(ratio, ratio);
context.translate(0.5, 0.5);
```

