

# css布局

## 浮动（Float）

## 定位（Positioning）

## 弹性布局（Flex Layout）

弹性盒子布局是一种**一维布局**，就是内容是按行或者列来布局

``` css
.container {
  display: -webkit-box;
  display: ms-flexbox;
  display: flex;
}
```

![flex基本概念](img\flex基本概念.png)

### 容器属性

#### 1. flex-direction

决定主轴的方向（即项目的排列方向）

``` css
flex-direction: column | column-reverse | row | row-reverse;
```

![direction](img\direction.png)

#### 2. flex-wrap

如果一条轴线排不下，如何换行

``` css
flex-wrap: nowrap | wrap | wrap-reverse;
```

![wrap](img\wrap.png)

#### 3. flex-flow

`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`

``` css
flex-flow: <flex-direction> || <flex-wrap>;
```

#### 4. justity-content

定义了项目在主轴上的对齐方式

``` css
justity-content: flex-start | flex-end | center | space-between | space-around;
```

![jusitify](img\jusitify.png)

#### 5. align-items

定义项目在交叉轴上如何对齐

``` css
align-items: flex-start | flex-end | center | baseline | stretch（延伸）;
```

![aligin-items](img\aligin-items.png)

#### 6. align-content

定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用

``` js
 align-content: flex-start | flex-end | center | space-between | space-around | stretch;
```

![align-content](img\align-content.png)

### 项目属性

#### 1. flex-grow

定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大

``` css
flex-grow: <number>;
```

如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

![flex-grow](img\flex-grow.png)

#### 2. flex-shrink

定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小

``` css
flex-shrink: <number>;
```

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。

![flex-shrink](img\flex-shrink.jpg)

#### 3. flex-basis

定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

```css
flex-basis: <length> | auto;
```

它可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间。如：`flex-basis: 350px`

#### 4. flex

`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

```css
flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ];
```

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)

#### 5. align-self

允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`

```css
align-self: auto | flex-start | flex-end | center | baseline | stretch;
```

![align-self](img\align-self.png)

## 网格布局（Grid Layout）

网格布局是一种用来进行**二维布局**的技术，按照行和列来布局

```css
.container {
  display: grid;
  grid-template-columns: 200px 200px 200px;
  grid-template-rows: 200px; 200px;
}
```





