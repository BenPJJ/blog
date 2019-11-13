# CMS

## CMS是什么

一个在线编辑网页的web服务器（基于php）

测试地址：

>  https://zsys.office.bzdev.net/admin/cms/index/index 

线上地址：

>  https://zsys.bozhong.com/cms/index/index 

## CMS的page、block

- page 

  用来发布网页、发布地址需要后端代理后才能正确访问

- block

  模块内容，例如pc头部、pc尾部、wap头部、wap尾部

## 变量说明

``` js
WWW_SEEDIT_COM => http://www.bozhong.com
SOURCE_SEEDIT_COM => http://scdn.bozhong.com/source
SCDN_SEEDIT_COM => http://source.bozhong.com
BBS_SEEDIT_COM => http://bbs.bozhong.com
```

## 函数说明

因为cms 基于php开发的，所以里面内置了一些php函数

-  RM_SCHEME 函数

  去除地址协议头

  ``` js
  RM_SCHEME(SOURCE_SEEDIT_COM) => //scdn.bozhong.com/source
  ```

  ``` html
  <a href="<?=RM_SCHME(SOURCE_SEEDIT_COM);?>/thread-123.html">点击跳转到帖子页</a>
  ```

-  Seedit_Func::checkmobile函数 

   判断当前是否是移动端访问，用于根据环境加载不同 block 

  ``` js
  Seedit_Func::checkmobile()
  ```

## Example

### wap端

``` js
<?php
  $isPc = Seedit_Func::checkmobile() ? false : true;
?>
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0" />
  <!-- <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1"> -->
  <title></title>
  <script src="//res.wx.qq.com/open/js/jweixin-1.2.0.js"></script>
  <script src="//source.bozhong.com/common/js/config.js"></script>
  <?php if ($isPc) { ?>
	  <link rel="stylesheet" type="text/css" href="<?=RM_SCHEME(SOURCE_SEEDIT_COM)?>/common/css/common_hf.min.css" />
    <script src="//scdn.bozhong.com/source/common/js/jquery.nohttp.min.js"></script>
    <script type="text/javascript">
      seajs.use("<?=RM_SCHEME(SOURCE_SEEDIT_COM)?>/common/js/common_nav_2016.js");
    </script>
  <?php } else { ?>
    <script>
      // rem
      (function(scope){
        // 下面750对应设计稿的宽度
        // document.body.innerHTML = window.innerWidth;
        var ua = navigator.userAgent.toLocaleLowerCase();
        if (!/(iPhone|iPad|iPod|iOS|Android|SymbianOS)/i.test(ua)) return false
        var eventName = 'onorientationchange' in scope ? 'orientationchange' : 'resize';
        var howLong = /chrome|firefox|ucbrowser|mqqbrowser/.test(ua) || (/safari/.test(ua) && /iphone/.test(ua)) ? 0 : 300;
        // app打开浏览窗体时可能第一时间无法获取浏览器宽度, 需循环
        var loop = function() {
          var winWidth = document.documentElement && document.documentElement.clientWidth ? document.documentElement.clientWidth : (window.screen ? window.screen.width : 0);
          var docWidth = window.innerWidth;
          // 宽度获取不成功延时执行
          if (!winWidth && !docWidth) return setTimeout(function() {
            loop();
          }, 100);
          var _width = !docWidth || (winWidth && winWidth < docWidth) ? winWidth : docWidth; // 兼容部分奇怪的安卓机
          document.documentElement.style.fontSize = (_width / 750 * 40) + 'px';
          scope.addEventListener(eventName, function(){
            clearTimeout(scope.orientationChangedTimeout);
            scope.orientationChangedTimeout = setTimeout(function(){
              document.documentElement.style.fontSize = (_width / 750 * 40) + 'px';
            }, howLong);
          }, false);
        };
        loop();
    }(window));
    </script>
  <?php } ?>
  <script>
    
    // 重定向后css/js需绝对路径引入
    // chunks默认注入判断为开发环境或不需要重定向
    ;

    var matched = window.location.href.match(/\/\/(\w*).([\w.]*)(\/\w*\/\w*)?/);
    var domain = '';
    if (/bozhong.com/.test(matched[0])) {
      domain = '//scdn.bozhong.com/source';
    } else if (/fe.office.bzdev.net/.test(matched[0])) {
      domain = '//fe.' + matched[2] + matched[3];
    } else {
      domain = '//source.' + matched[2];
    }

    var baseHref = document.createElement('base');
    // 按项目路径修改basehref路径_filePath，如activity/health，_filepath改成'/activity/health/'
    baseHref.href = domain + '/activity/2019publicwelfare/';

    document.head.appendChild(baseHref);
    
  </script>
  <script>
    var _hmt = _hmt || [];
    window._hmt = _hmt;
    (function() {
      var hm = document.createElement("script");
      hm.src = "//hm.baidu.com/hm.js?e31eaebaa37e0f895f2fdda58cc11de4";
      var s = document.getElementsByTagName("script")[0];
      s.parentNode.insertBefore(hm, s);
    })();
  </script>
</head>
<body   <?php echo $isPc ?>>
  <?php if ($isPc) { ?>
    <?=B('COMMON_头部_2016')?>
  <?php } ?>
  <div id="app">
  </div>
  
  <script type="text/javascript">
    var files = ["../../common/js/config.js","manifest.js?651403e3c14cdd4e659e","vendor.js?0d7fb07b98cc0ba2e9ef","main.js?fccde568dc34a86b4bac"];
    var queueIndex = 0;
    function loadScript (src, next) {
      var script = document.createElement('script');
      script.src = src;
      document.body.appendChild(script);
      script.onload = function () {
        if (next) {
          next();
        }
      };
    }
    function loadScriptLoop () {
      loadScript(files[queueIndex], function () {
        queueIndex += 1;
        if (queueIndex < files.length) {
          loadScriptLoop();
        }
      });
    }
    loadScriptLoop();
  </script>
</body>
</html>
```

