# Cookie

## 1. http 协议

- HTTP：超文本传输协议，用于从 web 服务器传输超文本到本地浏览器的传输协议，它是一个无状态的协议

## 2. cookie 的概念

- cookie：是指缓存在本地客户端的数据

## 3. cookie 的基本操作

- cookie 基本操作包括增、删、改、查四个部分

``` javascript
// 设置 cookie
document.cookie = "username=ben"

// 设置 cookie 时间
var oDate = new Date()
oDate.setDate(oDate.getDate() + 3)
document.cookie = "username=ben;expires="+oDate

// 查询 cookie
console.log(document.cookie)

// 修改 cookie
document.cookie = "username=ben"
document.cookie = "username=ben1"    

// 删除 cookie
var oDate = new Date()
oDate.setDate(oDate.getDate() - 1)
document.cookie = "username=ben;expires="+oDate
```

## 4. cookie 的封装

- setCookie()
- getCookie()
- removeCookie()

``` javascript
// 设置 cookie
function setCookie(name, value, day) {
  var oDate = new Date()
  oDate.setDate(oDate.getDate() + day)
  document.cookie = name + "=" + value + ";expires=" + oDate
}

setCookie("name1", "ben1", 1)
setCookie("name2", "ben2", 1)
console.log(document.cookie)

// 拿到 cookie
function getCookie(name) {
  var str = document.cookie
  var arr = str.split('; ')

  for (var item in arr) {
    var arr1 = arr[item].split('=')

    if (arr1[0] === name) {
      return arr1[1]
    }
  }
}

console.log(getCookie('name1'))

// 删除 cookie
function removeCookie(name) {
  setCookie(name, 1, -1)
}

removeCookie('name1')
console.log(getCookie('name1'))
```

## 5. 七天免登陆案例

``` javascript
<style>
  * {
      margin: 0;
      padding: 0;
    }
  .box{
      width: 400px;
      height: 300px;
      line-height: 50px;
      border: 1px solid #fc9;
      background-color: #fc9;
      margin: 50px auto;
      padding: 50px 0;
      box-sizing: border-box;
      text-align: center;
    }
</style>

<body>
    <div class="box">
        用户名：<input type="text" placeholder="请输入你的名字"></br>
        密&nbsp;&nbsp;&nbsp;码：<input type="password"></br>
        <label for=""><input type="checkbox" id="checkbox">七天免登陆</label></br>
        <input type="button" value="登陆">
    </div>
</body>

<script src="./common.js"></script>
<script>
    var aInput = document.getElementsByTagName('input')

    if (getCookie('username')) {
        aInput[0].value = getCookie('username')
        aInput[1].value = getCookie('password')
    }

    aInput[3].onclick = function () {
        var username = aInput[0].value
        var password = aInput[1].value

        if (aInput[2].checked) {
            setCookie('username', username, 7)
            setCookie('password', password, 7)
        }
    }
</script>
```

common.js

``` javascript
function setCookie(name, value, day) {
    var oDate = new Date()
    oDate.setDate(oDate.getDate() + day)
    document.cookie = name + '=' + value + ';expires=' + oDate
}

function getCookie(name) {
    var str = document.cookie
    var arr = str.split('; ')
    for (var item in arr) {
        var arr1 = arr[item].split('=')
        if (arr1[0] === name) {
            return arr1[1]
        }
    }
}

function removeCookie(name) {
    setCookie(name, 1, -1)
}
```

