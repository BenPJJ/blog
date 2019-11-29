# address

获取当前的机器ip、mac、dns服务器

## 安装

``` shell
npm install --save-dev address
```

## 基本配置

``` js
const address = require('address');
address.ip();
address.ipv6();
address.mac((err, addr) => {
  console.log(addr);
});
```

## example

- 私有IP地址范围：
  - A：10.0.0.0 ~10.255.255.255
  - B：172.16.0.0 ~ 172.31.255.255
  - C：192.168.0.0. ~ 192.168.255.255

``` js
// 获取ip
const getAddressIP = () => {
  let lanUrlForConfig = address.ip();
  if (!/^10[.]|^172[.](1[6-9]|2[0-9]|3[0-1])[.]|^192[.]168[.]/.test(lanUrlForConfig)) {
    lanUrlForConfig = undefined;                  
  }
  return lanUrlForConfig;
}
```

