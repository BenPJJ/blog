# hash和history模式

## 一、hash模式和history模式的区别

### 1. 通俗理解

- hash模式url里面永远带着#号，我们在开发当中默认使用这个模式。那么什么时候要用history模式呢？如果用户考虑url的规范那么就需要使用history模式，因为history模式没有#号，是个正常的url适合推广宣传。

- 其功能也是有区别，比如在开发app的时候有分享页面，那么这个分享出去的页面就是vue或是react做的，把这个页面分享到第三方的app里，有的app里面url是不允许带有#号，所以要将#号去除那么就要使用history模式，但是使用history模式还有一个问题就是，子啊访问二级页面的时候，做刷新操作，会出现404错误，那么就需要和后端人配合让他配置一下apache或是nginx的url重定向，重定向到你的首页路由上就ok啦

### 2. 官方

hash与history的区别

|          | hash                       | history          |
| -------- | -------------------------- | ---------------- |
| url显示  | 有#，很Low                 | 无#，好看        |
| 回车刷新 | 可以加载到hash值对应页面   | 一般就是404掉了  |
| 支持版本 | 支持低版本浏览器和IE浏览器 | HTML5新推出的API |

### 3. 原理

- hash模式（前端路由）

  这个#就是hash符号，中文名哈希符或锚点，哈希符后面的值，称之为哈希值。

  路由的哈希模式其实是利用了window可以监听onhashchange事件，也就是说你的url中的哈希值（#后面的值）如果发生变化，前端是可以做到监听并做一些响应（搞点事情），这么一来，即使前端并没有发起http请求他也能够找到对应页面的代码块进行按需加载。

- history模式

  - H5新推出pushState与replaceState，这两个神器的作用就是可以将url替换并且不刷新页面，好比挂羊头卖狗肉，http并没有去请求服务器该路径下的资源，一旦刷新就会暴露这个实际不存在的“羊头”，显示404

  - 如何去解决history模式下刷新报404的弊端呢

    这就需要服务器端做点手脚，将不存在的路径请求重定向到入口文件（index.html），前后端联手，齐心协力做好“挂羊头卖狗肉”的完美特效。

总之，pushState方法不会触发页面刷新，只是导致history对象发生变化，地址栏会有反应

### 4. 总结

传统的路由指的是：当用户访问一个url时，对应的服务器会接收这个请求，然后解析url中的路径，从而执行对应的处理逻辑。这样就完成了一次路由分发。

而前端路由是不涉及服务器的，是前端利用hash或者HTML5的history API来实现的，一般用于不同内容的展示和切换。

history模式下，build之后本地index.html打开是无效的

hash模式下，build之后本地index.html打开正常

## 二、next()

next()跳转到指定路径时会无限循环

``` js
// 下面的写法正确
beforeRouteLeave(to, from, next) {
    console.log('离开路由');
    if(to.fullPath === '/home') {
        next();
    } else {
        next('/home');
    }
}
```

这个是组件路由，我想实现的效果是在这个页面点击浏览器的返回按钮后要返回/home页面而不是上一个页面

```js
// 下面的写法会死循环
beforeRouteLeave(to, from, next) {
    console.log('离开路由');
    next('/home');
}
```

## 三、使用公司的脚手架webpack-bz

当使用history 模式时，需要通知后端做相应的配置

### 当前域名

``` js
# source.xxx.com
location /activity/wiki/ {
  try_files $uri $uri/ /activity/wiki/index.html;
}
```

### 代理跨域名

``` js
# m.xxxx.com
location ^~ /wiki/ {
  proxy_set_header Host source.xxxx.com;
  include proxy_params;
  proxy_pass https://127.0.0.1/activity/wiki/;
}
```

