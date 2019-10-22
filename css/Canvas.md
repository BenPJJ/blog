# Canvas

## 一、介绍

一个可以使用脚本（通常为JavaScript）在其中绘制图像的HTML 元素。它可以用来制作照片集或者简单（也不是那么简单）的动画，甚至可以进行实时视频处理和渲染。Canvas 是由HTML 代码配合高度和宽度属性而定义出的可绘制区域。

## 二、基本使用

- canvas 标签的使用

  ``` html
  <!-- canvas 默认宽度300px 150px css属性同样可以更改宽度但如果和初始化宽度比不统一会出现变形的问题，建议不要使用css定宽高-->
  <canvas id="target" width="300" height="150">
  	// 不支持canvas标签会显示该内容~
  </canvas>
  ```

- canvas 方法检查支持性

  ``` js
  // canvas 标签需要考虑浏览器版本兼容性、同样其对应的方法也应该考虑不支持的处理方式
  var canvas = document.getElementById('target');
  if (canvas.getContext) {
    var ctx = canvas.getContext('2d');
  } else {
    alert('该浏览器版本过低，请更换~');
  }
  ```

- canvas 绘制图形


### 1. 坐标系

![canvas](img\canvas.png)

### 2. 矩形

``` js
fillRect(x, y, width, height) // 填充以(x, y)为起点宽高分别为width、height的矩形，默认为黑色
stokeRect(x, y, width, height) // 绘制一个空心(x, y)为起点宽高分别为width、height的矩形
clearRect(x, y, width, height) // 清除以(x, y)为起点宽高分别为width、height的矩形，为透明
```

### 3. 路径

``` js
beginPath() // 新建一条路径一旦创建成功，绘制命令将转移到新建的路径上
moveTo(x, y) // 移动画笔到(x, y)点开始后面的绘制工作
closePath() // 关闭该路径，将绘制指令重新转移到上下文
stroke() // 将绘制的路径进行描边
fill() // 将绘制的封闭区域进行填充
```

JavaScript代码实例：

``` js
let canvas = this.$refs.target;
let ctx = canvas.getContext('2d');
ctx.moveTo(100, 10);
ctx.lineTo(200, 10);
ctx.lineTo(200, 100);
ctx.lineTo(100, 100);
ctx.lineTo(100, 10);
ctx.fill();
ctx.stroke();
```





### 4. 圆弧

``` js
arc( x , y , r , startAngle , endAngle ,  anticlosewise ) // 以(x,y)为圆心 r为半径的圆  绘制startAngle弧度 到endAngle弧度的圆弧 anticlosewise默认为false 即顺时针方向 true为逆时针方向

arcTo( x1 , y1 , x2 , y2 , radius ) //根据 两个控制点 (x1,y1) 和 (x2, y2)以及半径绘制弧线 同时连接两个控制点
```

- arc

  JavaScript代码实现:

  ```js
  ctx.beginPath();
  ctx.arc(10, 10, 5, 0, 2*Math.PI);
  ctx.stroke();
  ```

  ![canvas_arc](img\canvas_arc.png)

- arcTo

  JavaScript代码实现：

  ```js
  ctx.moveTo(20,20);           
  ctx.lineTo(100,20);          
  ctx.arcTo(150,20,150,70,50); 
  ctx.lineTo(150,120);        
  ctx.stroke();  
  ```

  ![canvas_arcTo](img\canvas_arcTo.png)

### 5. 贝塞尔曲线

- 一次贝塞尔曲线其实是一条直线

  ![canvas_first_curve](img\canvas_first_curve.gif)

- 二次贝塞尔曲线

  ```js
  quadraticCurveTo( cp1x, cp1y , x ,y )   // (cp1x,cp1y) 控制点    (x,y)结束点
  ```

  JavaScript代码实现：

  ```js
  ctx.moveTo(20,20);            
  ctx.quadraticCurveTo(50, 0, 100, 100);    
  ctx.stroke();  
  ```

  ![canvas_first_curve](img\canvas_second_curve.gif)

- 三次贝塞尔曲线

  ``` js
  bezierCurveTo( cp1x, cp1y ,cp2x , cp2y ,x , y )//（cp1x,cp1y）控制点1   (cp2x,cp2y) 控制点2  (x,y)结束点
  ```

  JavaScript代码实现：

  ```js
  ctx.moveTo(20,20);            
  ctx.bezierCurveTo(50, 0, 100, 100, 150, 20);    
  ctx.stroke();  
  ```

  ![canvas_first_curve](img\canvas_third_curve.gif)

### 6. 样式添加

- fillStyle

  ``` js
  fillStyle = color // 可以为颜色值、渐变对象
  ```

  JavaScript代码实现：

  ``` js
  ctx.fillStyle = '#f025db';
  ctx.fillStyle = 'red';
  ```

- strokeStyle

  ``` js
  strokeStyle = color // 可以为颜色值、渐变对象
  ```

  JavaScript代码实现：

  ``` js
  ctx,strokeStyle = 'red';
  ctx,strokeStyle = '#f025db';
  ```

- lineWidth

  ``` js
  linewidth = value // 线宽
  ```

  JavaScript代码实现：

  ``` js
  ctx.lineWidth = 5;
  ```

- lineCap

  ``` js
  lineCap = type (butt、round、square) // 线条末端样式，依次是方形、圆形（突出）、方形（突出）
  ```

  JavaScript代码实现：

  ``` js
  ctx.lineCap = 'round';
  ```

  ![canvas_lineCap](img\canvas_lineCap.png)

- lineJoin

  ``` js
  lineJoin = type (round、bevel、miter) // 线条交汇处样式，依次是圆形、平角、三角形
  ```

  JavaScript代码实现：

  ``` js
  ctx.lineJoin = 'round';
  ```

  ![canvas_lineJoin](img\canvas_lineJoin.png)











