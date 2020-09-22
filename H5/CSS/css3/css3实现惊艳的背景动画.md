# css3实现惊艳的背景动画

## 1. 实现内部虚线边框

``` css
outline
```

代码实现：

``` html
<div>hello world</div>
```

``` js
div {
  width: 200px;
  height: 100px;
  line-height: 100px;
  outline: 1px dashed #fff;
  outline-offset: -10px;
  text-align: center;
  background-color: #000;
  color: #fff;
}
```

![outline.png](img\outline.png)

## 2. 边框内圆角的实现

``` css
box-shadow
```

代码实现：

``` html
<div></div>
```

``` css
div {
  width: 200px;
  height: 100px;
  background-color: #000;
  box-shadow: 0 0 0 10px gray;
  border-radius: 10px;
  margin: 0 auto;
}
```

![shadow](img\shadow.png)

## 3. 实现条纹背景与进度条

``` css
linear-gradient、repeating-linear-gradient
```

代码实现：

``` html
<div><div>
```

``` css
div {
  width: 200px;
  height: 20px;
  background: linear-gradient(to right, #fb3 50%, #58a 0);
  background-size: 20px;
  border-radius: 10px;
  margin: 50px auto;
}
```

![linear-gradient](img\linear-gradient.png)

``` css
div {
  width: 200px;
  height: 20px;
  background: linear-gradient(45deg, #fb3 25%, #58a 0, #58a 50%, #fb3 0, #fb3 75%, #58a 0);
  background-size: 50px 50px;
  border-radius: 10px;
  margin: 50px auto;
}
```

![linear-gradient-deg](img\linear-gradient-deg.png)

``` css
div {
  width: 200px;
  height: 20px;
  background: repeating-linear-gradient(60deg, #fb3, 15px, #58a 0, #58a 30px);
  border-radius: 10px;
  margin: 50px auto;
}
```

![repeat-linear-gradient](img\repeat-linear-gradient.png)

## 4. 复杂的背景图案

``` css
linear-gradient、repeating-linear-gradient、radial-gradient
```

代码实现：

``` html
<div></div>
```

``` css
div {
  width: 200px;
  height: 200px;
  background-color: #000;
  border-radius: 10px;
  margin: 50px auto;
  background-image: linear-gradient(rgba(255,255,255, 1) 2px,transparent 0),
                      linear-gradient(to right, rgba(255, 255, 255, 1) 2px, transparent 0),
                      linear-gradient(rgba(255,255,255, .2) 1px,transparent 0),
                      linear-gradient(to right, rgba(255, 255, 255, .2) 1px, transparent 0);
  background-position: -50px -50px; 
  background-size: 100px 100px, 100px 100px, 100% 10px, 10px, 100%;
}
```

![linear-gradient-complex](img\linear-gradient-complex.png)

代码实现：

利用背景渐变实现棋盘图案

``` html
<div></div>
```

``` css
div {
  width: 200px;
  height: 200px;
  border-radius: 10px;
  margin: 50px auto;
  background-image: linear-gradient(45deg, rgba(0, 0, 0, .25) 25%, transparent 0, transparent 75%, rgba(0, 0, 0, .25) 0),
                      linear-gradient(45deg, rgba(0, 0, 0, .25) 25%, transparent 0, transparent 75%, rgba(0, 0, 0, .25) 0);
  background-position: 0 0, 25px 25px;
  background-size: 50px 50px;
}
```

![linear-gradient-complex02](img\linear-gradient-complex02.png)

代码实现：

利用css3多背景和position实现红绿灯和背景色块移动

## 5. 折角效果

``` css
linear-gradient
```

