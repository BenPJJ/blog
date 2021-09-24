# Chrome 插件（扩展）开发

## 6个核心概念

### 1. manifest.json（插件配置文件）

manifest.json文件是用来配置所有和插件相关的配置。必须放在根目录。其中`manifest_version` 、`name` 、`version` 为必填字段，`description` 、`icons` 为推荐字段。

``` json
{
  // 清单文件的版本，这个必须写，而且必须是2
  "manifest_version": 2,
  // 插件的名称
  "name": "demo",
  // 插件的版本
  "version": "1.0.0",
  // 插件的描述
  "description": "简单的Chrome扩展demo",
  // 图标，一般偷懒全部用一个尺寸的也没问题
  "icons": {
    "16": "img/icon.png",
    "48": "img/icon.png",
    "128": "img/icon.png"
  },
  "background": {
    "page": "backgroud.html"
    // "script": ["js/background.js"]
  },
  "browser_action": {
    "default_icon": "img/icon.png",
    "default_title": "这是一个示例Chrome插件",
    "default_popup": "popup.html"
  },
  //
  "content_scripts": [
    
  ],
  // 安全策略，默认情况下禁止使用eval或者Function构造函数，以及内联js，禁止载入外部脚本
  "content_security_policy": ""
  // 权限申请
  "permissions": [
    "contextMenus", // 右键菜单
    "tabs", // 标签
    "notifications", // 通知
    "webRequest", // web请求
    "storage", // 插件本地存储
    "http://*/*", // 可以通过executeScript或者insertCSS访问的网站
    "https://*/*" // 可以通过executeScript或者insertCSS访问的网站
  ],
  // 普通页面能够直接访问的插件资源列表
  "web_accessible_resources": ["js/inject.js"],
  // 插件主页（广告位）
  "homepage_url": "https://www.baidu.com",
  // 覆盖浏览器默认页面
  "chrome_url_overrides": {
    // 覆盖浏览器默认的新标签
    "newtab": "newtab.html"
  },
  // Chrome40以前的插件配置页写法
  "options_page": "options.html",
  // Chrome40以后的插件配置页写法，如果2种都存在，新版Chrome只读最后一个
  "options_ui": {
    "page": "options.html",
    // 添加一些默认的样式
    "chrome_style": true
  },
  // 向地址栏注册一个关键字以提供搜索建议（只能一个）
  "omnibox": {
    "keywrod": "go"
  },
  // 默认语言
  "default_locale": "zh_CN",
  // devtools页面入口（html文件）
  "devtools_page": "devtools.html"
}
```

### 2. content-scripts（插入到目标页面中执行的js）

content-scripts 其实就是Chrome 插件中向页面注入脚本的一种形式，通过content-scripts 可以向指定页面注入JS 和CSS

**缺陷：**

​	content-script 无法访问页面中的JS，虽然可以操作DOM，但是DOM 却不能调用conten-script，也就是无法在DOM 中通过绑定事件的方式（onclick and addEventListener 2中方式）调用content-script 中的代码。

**配置：**

``` json
{
  // 需要直接注入页面的JS
  "content-scripts": [
    {
      // "matches": ["http://*/*", "https://*/*"]
      // "<all_urls>" 表示匹配所有地址
      "matches": ["<all_urls>"],
      // 多个JS按顺序注入
      "js"： ["js/jquery-1.8.3.js", "js/content-script.js"],
  		// css注入小心，防止可能影响全局样式
  		"css": ["css/custom.css"],
  		// 代码注入的时间，可选值“document_start”、“document_end”、默认“document_idle”（表示页面空闲时）
  		"run_at": "document_start"
    }
  ]
}
```

content-scripts 和原始页面共享DOM，但是不共享JS，如果访问页面JS，只能通过injected js来实现。

**content-scripts 局限性：**

content-scripts 不能访问绝大部分chrome.xxx.api。

除了下面4种：

- chrome.extension(getURL, inIncognitoContext, lastError, onRequest, sendRequest)
- chrome.i18n
- chrome.runtime(content, getManifest, getURL, id, onConnect, onMessage, sendMessage)
- chrome.storage

### 3. background（在chrome后台中运行的程序）

background 是一个常驻的页面，它的生命周期是插件中所有类型页面中最长的，它随着浏览器的打开而打开，随着浏览器的关闭而关闭，所以通常把需要**一直运行的**、**启动就运行的**、**全局的代码**放在background里面

``` json
{
  // 会一直常驻的后台JS或后台页面
  "background": {
    // 2种指定方式，如果指定JS，那么会自动生成一个背景页
    “page”: "background.html"
    // "scripts": ["js/background.js"]
  }
}
```

### 4. event-pages

生命周期：

- 在被需要时（如：第一次安装、插件更新、有content-scripts 向它发送信息等）加载，在空闲时被关闭

``` json
{
  "background": {
    "scripts": ["js/event-pages.js"],
    "persistent": false
  }
}
```

### 5. popup（点击插件图标弹出的页面）

**定义：**

​	popup 是点击browser_action 或者page_action 图标时**打开一个小窗口网页**，焦点离开网页就立即关闭。

**生命周期：**

​	popup页面的生命周期一般很短（单击图片打开popup，焦点离开又立即关闭），如果需要长时间运行的代码不宜写在popup页面。

**权限：**

​	非常类似background，popup 中可以通过`chrome.extension.getBackgroundPage()` 获取background的window 对象。

**配置：**

``` json
{
  "browser_action": {
    "default_icon": "img/icon.png",
    "default_title": "这是一个示例Chrome插件",
    "default_popup": "popup.html"
  }
}
```

### 6. injected-script（content_script 注入到页面的js）

**定义：**

​	injected-script 指通过DOM 操作的方式向页面注入的一种JS。因为content-script 的缺陷，所以需要通过injected-sctipt 的方式来实现功能

**使用：**

​	在content-script 中通过DOM 方式向页面注入inject-script

``` js
funtion injectCustomJs(jsPath) {
  jsPath =jsPath || 'js/inject.js';
  var temp = document.createElement('script');
  temp.setAttribute('type', 'text/javascript');
  temp.src = chrome.extension.getURL(jsPath);
  temp.onload = function() {
    this.parentNode.removeChild(this);
  }
  document.head.appendChild(temp)
}
```

**配置：**

​	在web 中直接访问插件中的资源必须显示声明

```json
{
  // 普通页面能够直接访问的插件资源列表，如果不设置是无法直接访问
  "web_accessible_resources": ["js/inject.js"]
}
```

### 7. homepage_url

**定义：**

​	开发者或者插件主页设置

## 消息通信

### 1. popup & background

**注意：**

- background 访问popup 前提是popup已经打开

``` js
// background 配置 background.js
var views = chrome.extension.getViews({type: 'popup'});
if(views.length > 0) {
  console.log(views[0].location.href);
}
function test() {
  alert('我是background');
}

// browser_action 配置 popup.js
var bg = chrome.extension.getBackgroundPage();
bg.test();
alert(bg.document.body.innerHTML);
```

### 2. popup、background

### 3. content-script 主动发信息给后台

**注意：**

- content-script 先popup 主动发信息的前提是popup必须打开，否则需要利用background 作中转
- 如果background 和popup 同时监听，那么都可以同时收到信息，但是只有一个可以sendResponse，一个先发送了，那么另外一个再发送就无效

``` js
// content-script.js
chrome.runtime.sendMessage({greeting: '你好，我是conten-script呀，我主动发信息给后台'}, function(response) {
  console.log('收到来自后台的回复：' + response);
});

// background.js or popup.js
chrome.runtime.onMessage.addListener(function(request, sender, sendResponse) {
  console.log('收到来自content-script的信息');
  console.log(request, sender, sendResponse);
  sendResponse('我是后台，我已收到你的信息：' + JSON.stringify(request));
});
```

### 4. injected-script 和content-script



## 数据存储

**chrome.storage 分类：**

- chrome.storage.local 把数据保存在本地

- chrome.storage.sync 在chrome自己的用户体系里面把用户保存的插件信息进行服务器同步

**使用：**

``` js
chrome.storage.local.set({key: value}, function() {
	console.log('value is set to' + value);
});

chrome.storage.local.get(['key'], function(result) {
	console.log('value currently is' + result.key);
});

chrome.storage.sync.set({key: value}, function() {
	console.log('value is set to' + value);
});

chrome.storage.sync.get(['key'], function(result) {
	console.log('value currently is' + result.key);
});
```





## 重要api

```js
chrome.tabs.query
```

