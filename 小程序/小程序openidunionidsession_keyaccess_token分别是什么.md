# 小程序openid/unionid/session_key/access_token分别是什么

## code（用户登录凭证）

用于换取用户的`openid `和本次登录的会话密钥`session_key`

### 1. 获取

通过`wx.login` 经用户授权获得code

``` js
wx.login({
  success (res) {
    const code = res.code; // 微信用户登录凭证，五分钟有效
  },
  fail (err) {
    console.log(err);
  }
});
```

## OpenID（普通用户唯一标识）

**普通用户的标识，对当前应用唯一**

在关注者与公众号产生信息交互后，公众号可获得关注者`openid` ，**注意，不同的公众号`openid` 是不同的，不同的小程序`openid` 是不同的，公众号和小程序`openid` 也是不同的，`openid` 只对当前应用是唯一**

### 1. 作用

通过`openid`可以获得用户的基本信息，包括昵称、头像、性别、所在城市、语言和关注时间。小程序接入微信支付也需要`openid`

### 2. 获取

后台开发者通过使用`AppId & AppSecret & code` 调用` auth.code2Session接口` 获得` openid & session_key & unionid` ，其中`unionid` 根据情况决定是否返回，已关注或已授权即可返回

## UnionID（微信用户唯一标识）

用户唯一标识，前面讲到`openid` 在不同的应用中是不同的，但是开发者拥有多个应用，如何区分用户的唯一性？只要是同一个微信开放平台账号下的移动应用、网站应用和公众账号（包括小程序），用户的`	UnionID` 是唯一的

### 1. 使用unionid的前提

需要前往微信开放平台，将这些公众号和应用绑定到一个开放平台账号下，绑定后，一个用户虽然对多个公众号和应用有多个不同的`openid` ，但他对所有这些同一开放平台账号下的公众号和应用，只有一个`unionid`

### 2. 获取

- 通过` wx.getUserInfo`获取含`unionId`的加密数据，需要后台开发者进行解密
- 用户已关注公众号，`wx.login `和` auth.code2Session `可获得返回的`unionid`
- 用户已经授权登录过公众号或小程序，`wx.login` 和 `auth.code2Session` 可获得返回的`unionid`
-  支付完成可调用接口`getPaidUnionId`获取`unionid`，接口在支付行为的五分钟内有效

## session_key（本地登录的会话密钥）

通过 `wx.getUserInfo`获取微信用户数据`encryptedData`（含手机号码，被加密），后台开发者解密用户数据需要用到`session_key`

### 1. 获得

后台开发者通过使用 `AppId & AppSecret & code `调用 `auth.code2Session`接口 获得 `openid & session_key & unionid `(根据情况决定是否返回，已关注或已授权即可返回)

## access_token（小程序全局唯一后台调用凭证）

小程序全局唯一后台接口调用凭证，**调用绝大多数后台接口时都需使用access_token**

![区别](img\区别.jpg)