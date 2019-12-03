## vue中使用百度统计

因项目运营需求前端需要埋点，统计页面流量。

## 使用

### 1. 在index.html的head中引入代码

将代码按提示引入到页面，如果代码安装正确，**一般20分钟后**，可以查看网站分析数据

``` html
<head>
<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "//hm.baidu.com/hm.js?你的代码";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>
</head>
```

### 2. 监听路由变化，触出pv统计

#### 1. 正常

``` js
// vue-router
router.beforeEach((to, from, next) => {
  if (window._hmt && to.path) {
    window._hmt.push(['_trackPageview', '/#' + to.fullPath]);
  }
})
```

在控制台中查看统计是否发送成功

![router](img\router.png)

#### 2. 公司

> 学习文档：https://github.com/BozhongFE/blog/issues/1

路由百度统计pv、uv处理，必须指定`location.pathname` 路径，站内大部分地址代理过，如果不加会统计到M站首页根目录下面

``` js
# hash模式
router.afterEach((to, from, next) => {
  if (window._hmt && to.path) {
    const location = window.location;
    const pagePath = location.pathname + '#' + to.fullPath;
    window._hmt.push(['_trackPageview', pagePath]);
  }
});
```

``` js
# history模式
router.afterEach((to, from) => {
  if (window._hmt && to.path) {
    const location = window.location;
    const length = location.pathname.length - 1;
    const pagePath = `${location.pathname.substring(0, length)}${to.fullPath}`;
    window._hmt.push(['_trackPageview', pagePath]);
  }
});
```

### 3. vue中跳转外部链接的

> 文档查看：https://tongji.baidu.com/open/api/more?p=guide_trackEvent

``` html
<a @click="btn">点击按钮</a>
```

``` vue
methods: {
    btn(e) {
        e.preventDefault();
        window._hmt.push(['_trackEvent', '鹿啄泉', '首页', '马上查看']);
        setTimeout(() => {
          window.location.href = 'https://bbs.bozhong.com/thread-41698687-1-1.html';
        },300);
    }
}
```

