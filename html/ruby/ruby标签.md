# ruby标签

使用ruby 注释（中文注音或字符）

ruby 标签通常和rt 标签和rp 标签一起使用，rt 标签用来提供注释信息（如：拼音），rp 标签用来定义浏览器不支持ruby 标签时所显示的内容

## 格式

``` shell
<ruby>字符<rt>注解</rt></ruby>
```

## Example

``` html
<ruby>
  你<rp>(</rp><rt>ni</rt></rt><rp>)</rp>
</ruby>
```