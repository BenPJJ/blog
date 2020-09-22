# Canvas

>  https://www.canvasapi.cn/ 

## 一、介绍

一个可以使用脚本（通常为JavaScript）在其中绘制图像的HTML 元素。它可以用来制作照片集或者简单（也不是那么简单）的动画，甚至可以进行实时视频处理和渲染。Canvas 是由HTML 代码配合高度和宽度属性而定义出的可绘制区域。

## 二、API

### 1. 无分类

#### measureText(text)

用来测量文本的一些数据

#### clearRect(x, y, width, height)

清除画布

### 2. 路径

#### beginPath()

新建一条路径

#### closePath()

闭合路径

#### fill()

将绘制的封闭区域进行填充

#### moveTo(x, y)

移动画笔到(x, y)点开始后面的绘制工作

#### lineTo(x, y)

绘制直线以连接当前最后的字路径点

#### stroke()

将绘制的路径进行描边

#### setLineDash()

设置虚线样式

#### getLineDash()

获取当前虚线的样式

### 3. 圆弧

#### arc( x , y , r , startAngle , endAngle ,  anticlosewise )

以(x,y)为圆心 r为半径的圆  绘制startAngle弧度 到endAngle弧度的圆弧 anticlosewise默认为false 即顺时针方向 true为逆时针方向

![canvas_arc](img\canvas_arc.png)

#### arcTo( x1 , y1 , x2 , y2 , radius )

根据 两个控制点 (x1,y1) 和 (x2, y2)以及半径绘制弧线 同时连接两个控制点

![canvas_arcTo](img\canvas_arcTo.png)

### 4. 贝塞尔曲线

#### 一次贝塞尔曲线其实是一条直线

![canvas_first_curve](img\canvas_first_curve.gif)

#### quadraticCurveTo( cp1x, cp1y , x ,y ) 

二次贝塞尔曲线（cp1x,cp1y）控制点  (x,y)结束点

![canvas_first_curve](img\canvas_second_curve.gif)

#### bezierCurveTo( cp1x, cp1y ,cp2x , cp2y ,x , y )

三次贝塞尔曲线（cp1x,cp1y）控制点1   (cp2x,cp2y) 控制点2  (x,y)结束点

![canvas_first_curve](img\canvas_third_curve.gif)

### 5. 绘图形

#### 椭圆

##### ellipse(x, y, radiusX, radiusY, rotation, startAngle, endAngle, anticlockwise)

绘制椭圆

| 参数          | 类型            | 说明                                                       |
| ------------- | --------------- | ---------------------------------------------------------- |
| x             | Number          | 椭圆弧对应的圆心横坐标                                     |
| y             | Number          | 椭圆弧对应的圆心纵坐标                                     |
| radiusX       | Number          | 椭圆弧的长轴半径大小                                       |
| radiusY       | Number          | 椭圆弧的短轴半径大小                                       |
| rotation      | Number          | 椭圆弧的旋转角度，单位是弧度                               |
| starAngle     | Number          | 圆弧开始的角度，角度从横轴开始算，单位是弧度               |
| endAngle      | Number          | 圆弧结束的角度，单位是弧度                                 |
| anticlockwise | Boolean（可选） | 弧度的开始到结束的绘制是按照顺时针来算，还是按时逆时针来算 |

#### 矩形

##### fillRect(x, y, width, height)

填充以(x, y)为起点宽高分别为width、height的矩形，默认为黑色

##### strokeRect(x, y, width, height)

矩形描边效果

##### rect(x, y, width, height)

绘制矩形路径

### 6. 绘文字

#### fillText(text, x, y [, maxWidth])

填充文字

| 参数     | 类型           | 说明                 |
| -------- | -------------- | -------------------- |
| text     | String         | 用来填充的文本信息   |
| x        | Number         | 填充文本的起点横坐标 |
| y        | Number         | 填充文本的起点纵坐标 |
| maxWidth | Number（可选） |                      |

#### strokeText(text, x, y[, maxWidth])

文本描边效果

### 7. 绘制图片

#### drawImage(image, x, y, width, height)

 image为图片对象、从(x,y)处放置宽高分别为width height的图片 

#### drawImage(image, sx, sy, swidth, sheight, dx, dy, dwidth, dheight)

 切片前四个是定义图像源的切片位置和大小   后四个是定期切片的目标显示位置大小 

#### putImageData(image, dx, dy)

将给定image 对象的数据绘制到位图上

#### putImageData(image, dx, dy, dirtyX, dirtyY, dirtyWidth, dirtyHeight)

| 参数        | 类型                    | 说明                                   |
| ----------- | ----------------------- | -------------------------------------- |
| image       | Object                  | 图像像素信息                           |
| dx          | Number                  | 目标Canvas中被图像数据替换的起点横坐标 |
| dy          | Number                  | 目标Canvas中被图像数据替换的起点纵坐标 |
| dirtyX      | Number（可选），默认`0` | 图像数据渲染区域的左上角横坐标         |
| dirtyY      | Number（可选），默认`0` | 图像数据渲染区域的左上角纵坐标         |
| dirtyWidth  | Number（可选）          | 图像数据渲染区域的宽度                 |
| dirtyHeight | Number（可选）          | 图像数据渲染区域的高度                 |

#### getImageData(sx, sy, sWidth, sHeight)

获取指定位置的图像

### 8. 裁剪

#### clip()

只显示裁剪区域内部区域，先绘制剪裁路径，再执行`clip()` 方法

``` js
const context = canvas.getContext('2d');
const img = new Image();
img.src = require('../assets/img/head.jpg');
img.onload = () => {
  context.beginPath();
  context.moveTo(20, 20);
  context.lineTo(200, 80);
  context.lineTo(110, 150);
  context.clip();
  context.drawImage(img, 0, 0, 300, 400);
}
```

### 9. 渐变

#### createRadialCradient(x0, y0, r0, x1, y1, r1)

创建径向渐变

| 参数 | 类型   | 说明           |
| ---- | ------ | -------------- |
| x0   | Number | 起始圆的横坐标 |
| y0   | Number | 起始圆的纵坐标 |
| r0   | Number | 起始圆的半径   |
| x1   | Number | 结束圆的横坐标 |
| y1   | Number | 结束圆的纵坐标 |
| r1   | Number | 结束圆的半径   |

### 10. 状态保存 恢复

#### save()

保存

#### restore()

恢复

### 11. 动作

#### translate(x, y)

将canvas 的原点移动到（x, y）

#### rotate(angle)

顺时针方向旋转坐标轴 angle 弧度

#### scale(x, y)

将图形横向缩放x 倍、纵向缩放y 倍





### 



