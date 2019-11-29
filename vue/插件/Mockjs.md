# Mockjs

## 1. 安装

``` js
npm install --save mockjs
```

## 2. 引入文件

``` js
import Mock from 'mockjs';
```

## 3. 特性

- 数据类型丰富

  支持生成随机的文本、数字、布尔值、日期、邮箱、链接、图片、颜色等

- 拦截Ajax 请求

  不需要修改既有代码，就可以拦截Ajax 请求，返回模拟的响应数据。安全又便捷

## 4. 语法规范

### 数据模板定义规范

- **属性值是字符串String**

  ``` js
  'name|min-max': string
  ```

  重复`string `生成一个字符串，重复次数大于等于`min`，小于等于`max`

  ``` js
  'name|count': string
  ```

  重复`string`生成一个字符串，重复次数等于`count`

- **属性值是数字Number**

  ``` js
  'name|+1': number
  ```

  属性值自动加1，初始值为`number`

  ```js
  'name|min-max': number
  ```

  生成一个大于等于`min`、小于等于`max`的整数，属性值`number` 只是用来确定类型

  ```js
  'name|min-max.dmin-dmax': number
  ```

  生成一个浮点数，整数部分大于等于`min`、小于等于`max`，小数部分保留`dmin`到`dmax`位

  代码实现：

  ``` js
  Mock.mock({
      'number1|1-100.1-10': 1,
      'number2|123.1-10': 1,
      'number3|123.3': 1,
      'number4|123.10': 1.123
  })
  // =>
  {
      "number1": 12.92,
      "number2": 123.51,
      "number3": 123.777,
      "number4": 123.1231091814
  }
  ```

- **属性值是布尔值Boolean**

  ``` js
  'name|1': boolean
  ```

  随机生成一个布尔值，值为true、false的概率同样是1/2

  ``` js
  'name|min-max': value
  ```

  随机生成一个布尔值，值为`value`的概率是`min / (min + max)` ，值为`!value` 的概率是`max / (min + max)`

- **属性值是对象Object**

  ``` js
  'name|count': object
  ```

  从属性值`object` 中随机选取`count` 个属性

  ``` js
  'name|min-max': object
  ```

  从属性值`object` 中随机选取`min` 到`max` 个属性

- **属性值是数组Array**

  ``` js
  'name|1': array
  ```

  从属性值`array` 中随机选取1个元素，作为最终值

  ``` js
  'name|+1': array
  ```

  从属性值`array` 中顺序选取1个元素，作为最终值

  ``` js
  'name|min-max': array
  ```

  重复属性值`array` 生成一个新数组，重复次数大于等于`min` ，小于等于`max`

  ``` js
  'name|count': array
  ```

  重复属性值`array` 生成一个新数组，重复次数为`count`

- **属性值是函数Function**

  ``` js
  'name': function
  ```

  执行函数`function` ，取其返回值作为最终的属性值，函数的上下文为属性`name` 所在的对象

- **属性值是正则表达式RegExp**

  ``` js
  'name': 'regexp'
  ```

  根据正则表达式`regexp` 反向生成可以匹配它的字符串。

  代码实现：

  ``` js
  Mock.mock({
      'regexp1': /[a-z][A-Z][0-9]/,
      'regexp2': /\w\W\s\S\d\D/,
      'regexp3': /\d{5,10}/
  })
  // =>
  {
      "regexp1": "pJ7",
      "regexp2": "F)\fp1G",
      "regexp3": "561659409"
  }
  ```

### 数据占位符定义规范

占位符只是在属性值字符串中占个位置，并不出现在最终的属性值中

占位符的格式为：

``` js
@占位符
@占位符(参数[, 参数])
```

注意：

- 用`@` 来标识其后的字符串是占位符
- 占位符引用的是`Mock.Random` 中的方法
- 通过`Mock.Random.extend()` 来扩展自定义占位符
- 占位符也可以引用数据模板中的属性
- 占位符会优先引用数据模板中的属性
- 占位符支持相对路径和绝对路径

``` js
Mock.mock({
    name: {
        first: '@FIRST',
        middle: '@FIRST',
        last: '@LAST',
        full: '@first @middle @last'
    }
})
// =>
{
    "name": {
        "first": "Charles",
        "middle": "Brenda",
        "last": "Lopez",
        "full": "Charles Brenda Lopez"
    }
}
```

## 5. API

- Mock.mock(url, type, data)

  | 参数名   | 参数需求                 | 参数描述       | 例子                               |
  | -------- | ------------------------ | -------------- | ---------------------------------- |
  | url      | 可选：URL字符串或URL正则 | 拦截请求的地址 | /mock                              |
  | type     | 可选                     | 拦截Ajax       | GET、POST                          |
  | template | 可选：可以是对象或字符串 | 生成数据的模板 | {'data\|1-10':['mock']} 、'@EMAIL' |

  ``` js
  // 类型1： 名字|规则：内容
  Mock.mock({'data|1-4': '哑巴'})
  
  // 生成1-4 个哑巴字符串
  {
    data: "哑巴哑巴哑巴哑巴"
  }
  
  // 类型2：Mock自带模板
  Mock.mock('@province')
  
  // 随机生成一个省份
  "上海"
  ```

## 6. 例子

- 生成图片

``` js
'img': Mock.Random.image('200x400')
```



