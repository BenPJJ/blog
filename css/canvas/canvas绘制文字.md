## canvas绘制文字

canvas 提供了两种方法绘制文本：

## 第一种：

`fillText(text, x, y[, maxWidth])`

在指定位置的（x，y）位置填充指定的文本，绘制的最大宽度是可选的

## 第二种：

`strokeText(text, x, y[, maxWidth])`

在指定的位置绘制文本边框

## 文本样式

- `font = value`

  设置文本的尺寸，默认字体是`10px sans-serif`

- `textAlign = value`

  文本对齐选项，可选的值包括：`start` 、`end`、`left` 、`right`、`center` ，默认值为`start`

- `textBaseline = value`

  基线对齐选项，可选的值包括：`top` 、`hanging`、`middle` 、`alphabetic`、`ideographic` 、`bottom`，默认值为`alphabetic`

- `direction = value`

  文本方向，可选的值包括：`ltr` 、`rtl` 、`inherit` ，默认值为`inherit`

## 文本裁量

当需要更多文本细节时，使用`measureText()` 返回含文本特性的对象