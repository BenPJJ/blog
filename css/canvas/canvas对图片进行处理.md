# canvas对图片进行处理

## 主要API

- drawImage() 绘制图像
- getImageData() 获取图像数据
- putImageData() 重写图像数据
- toDataURL() 导出图像

### drawImage()

- `context.drawImage(img, x, y)` 

  在画布上定位图像

- `context.drawImage(img, x, y, width, height)`

  在画布上定位图像，并规定图像和宽度和高度

- `context.drawImage(img, sx, sy, swidth, sheight, x, y, width, height)`

  剪切图像，并在画布上定位被剪切的部分

| 参数    | 描述                                         |
| :------ | :------------------------------------------- |
| img     | 规定要使用的图像、画布或视频。               |
| sx      | 可选。开始剪切的 x 坐标位置。                |
| sy      | 可选。开始剪切的 y 坐标位置。                |
| swidth  | 可选。被剪切图像的宽度。                     |
| sheight | 可选。被剪切图像的高度。                     |
| x       | 在画布上放置图像的 x 坐标位置。              |
| y       | 在画布上放置图像的 y 坐标位置。              |
| width   | 可选。要使用的图像的宽度。（伸展或缩小图像） |
| height  | 可选。要使用的图像的高度。（伸展或缩小图像） |

### getImageData()

- `var ImageData = context.getImageData(x, y, width, height)`

  获取画布指定矩形范围内的像素数据

  - ImageData 对象，该对象拷贝了画布指定矩形的像素数据

| 参数   | 描述                            |
| :----- | :------------------------------ |
| x      | 开始复制的左上角位置的 x 坐标。 |
| y      | 开始复制的左上角位置的 y 坐标。 |
| width  | 将要复制的矩形区域的宽度。      |
| height | 将要复制的矩形区域的高度。      |

![getImageData](img\getImageData.png)

### putImageData()

- ` context.putImageData(imgData,x,y,dirtyX,dirtyY,dirtyWidth,dirtyHeight) `

| 参数        | 描述                                                  |
| :---------- | :---------------------------------------------------- |
| imgData     | 规定要放回画布的 ImageData 对象。                     |
| x           | ImageData 对象左上角的 x 坐标，以像素计。             |
| y           | ImageData 对象左上角的 y 坐标，以像素计。             |
| dirtyX      | 可选。水平值（x），以像素计，在画布上放置图像的位置。 |
| dirtyY      | 可选。水平值（y），以像素计，在画布上放置图像的位置。 |
| dirtyWidth  | 可选。在画布上绘制图像所使用的宽度。                  |
| dirtyHeight | 可选。在画布上绘制图像所使用的高度。                  |

### toDataURL()

- `var dataURL = canvas.toDataURL(type, encoderOptions)`

| 参数           | 描述                                                         |
| :------------- | :----------------------------------------------------------- |
| type           | 可选。图片格式，默认为 image/png。                           |
| encoderOptions | 可选。在指定图片格式为 image/jpeg 或 image/webp的情况下，可以从 0 到 1 的区间内选择图片的质量。如果超出取值范围，将会使用默认值 0.92。其他参数会被忽略。 |

## Example

``` html
<canvas id="canvas" width="600" height="600"></canvas>
```

``` js
createImage() {
  const canvas = document.getElementById('canvas'),
        context = canvas.getContext('2d');
  const image = new Image();
  image.src = require('../../assets/img/result_graduation.png');
  image.onload = () => { // 这处操作需要在图片加载成功后执行，否则图片将处理无效
    context.drawImage(image, 0, 0);
    // ... 需要操作的方法
  };
},
```

### 灰度影响

``` js
// 灰度影响
greyEffect(context) {
  const imageData = context.getImageData(0, 0, canvas.width, canvas.height);
  let pixelData = imageData.data;
  for (let i = 0; i < canvas.width*canvas.height; i += 1) {
    const r = pixelData[i * 4 + 0];
    const g = pixelData[i * 4 + 1];
    const b = pixelData[i * 4 + 2];
    const grey = r*0.3+g*0.59+b*0.11; // 这个算法是图像学家研究出对RGB深浅的最好值
    pixelData[i * 4 + 0] = pixelData[i * 4 + 1] = pixelData[i * 4 + 2] = grey;
  }
  context.putImageData(imageData, 0, 0);
},
```

### 黑白滤镜

是指图像上只有白色，黑色，也就是rgb(255, 255, 255)，或是rgb(0, 0, 0)

```js
// 黑白滤镜
blackEffect(context) {
  const imageData = context.getImageData(0, 0, canvas.width, canvas.height);
  const pixelData = imageData.data;
  for (let i = 0; i < canvas.width * canvas.height; i += 1) {
    const r = pixelData[i * 4 + 0];
    const g = pixelData[i * 4 + 1];
    const b = pixelData[i * 4 + 2];
    const grey = r*0.3+g*0.59+b*0.11;
    let pv = 0;
    if (grey > 125) {
      pv = 255;
    } else {
      pv = 0;
    }
    pixelData[i * 4 + 0] = pixelData[i * 4 + 1] = pixelData[i * 4 + 2] = pv;
  }
  context.putImageData(imageData, 0, 0);
},
```

### 反色滤镜

是指图像上的每一个点的RGB值修改为255-原来的值

``` js
reverseEffect(context) {
  const imageData = context.getImageData(0, 0, canvas.width, canvas.height);
  const pixelData = imageData.data;
  for (let i = 0; i < canvas.width * canvas.height; i += 1) {
    const r = pixelData[i * 4 + 0];
    const g = pixelData[i * 4 + 1];
    const b = pixelData[i * 4 + 2];
    pixelData[i * 4 + 0] = 255 - r;
    pixelData[i * 4 + 1] = 255 - g;
    pixelData[i * 4 + 2] = 255 - b;
  }
  context.putImageData(imageData, 0, 0);
},
```

## 组件

>  https://github.com/BozhongFE/bz-canvas2img 

## 报错

### 一：

> Failed to execute 'toDataURL' on 'HTMLCanvasElement': Tainted canvases may not be exported.

#### 分析原因：

canvas 绘制图片，由于浏览器的安全考虑，如果在使用canvas 绘图的过程中，使用到了外域的图片资源，那么在`toDataURL()` 时会抛出安全异常：

#### 解决方案：

**一：**

如果想使用`toDataURL()` 生成图片文件的话，在canvas 绘图过程中使用的图片应该是当前域下的

**二：**

访问的服务器允许，资源跨域使用，也就是说设置了CORS 跨域配置，`Access-Control-Allow-Origin`

然后在客户端访问图片资源的时候

``` js
const img = new Image();
// [切记]先setAttribute 在url 就不会有问题了
img.setAttribute('crossOrigin', 'anonymous');
img.src = url;
```

