# h5与ios、android交互

## h5向ios、android传参

``` js
const ua = window.navigator.userAgent;
isiOS = /(iPhone|iPod|iOS)/i.test(ua);
isAndroid = /Android/i.test(ua);
```

**ios**

给ios 传递参数需要用`window.webkit.messageHandlers.注册的方法名.postMessage({body: 传输的数据})` 来给native 发送信息

``` js
window.webkit.messageHandlers.methodsName.postMessage({"key":"parameter"})
```

**android**

给Android 传递参数需要用`window.Android.注册的方法名({body: 传输的方法})` 来给native 发送信息

``` js
window.Android.methodsName({"key":"parameter"})
```

## ios、android调用js方法

把写好的代码封装到一个方法里，跟ios 和android 定义好方法名就好

``` js
function showAlert() {
  alert('被截获到了!');
}
```

## example

``` js
if (isiOs && window.webkit) {
  window.webkit.messageHandlers.getPhoneInfo.postMessage(null);
  window.getPhoneInfoResult = function(phoneInfo) {
    typeof phoneInfo === 'string' && (phoneInfo = JSON.parse(phoneInfo));
  }
} else if (isAndroid && window.bzinner) {
  let phoneInfo = window.bzinner.getPhoneInfo();
  typeof phoneInfo === 'string' && (phoneInfo = JSON.parse(phoneInfo));
}
```

