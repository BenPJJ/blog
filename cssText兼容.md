# cssText兼容

在某些浏览器中（如Chrome），赋什么值，就返回什么值。在ie 中则比较特殊，它会格式化输出、会把属性大写、会改变属性顺序、会去掉最后一个分号

一般情况下我们用js 设置元素对象的样式会使用这样的形式：

``` css
element.style.width = "20px";
element.sytle.height = "20px";
....
```

样式一多，代码就很多；而且通过JS 来覆写对象的样式是比较典型的一种销毁原样式并重建的过程，这种销毁和重建，都会增加浏览器的开销

``` css
var cssText += ";font-weight: bold;color: red;"
//ie
element.style.cssText = cssText;
// firefox
element.setAttribute("style", cssText);
```

