# 使用github上的库
---
> 开源的项目，发现需求不太满足，需要添加自己的需求
### - 直接引用github上的项目
在`package.json`中将对应的源改为github上的项目地址，就可以替换掉原来的npm源，而github一般都比较稳定，直接引用也不会有很大问题
- 格式：
  - `git+ssh//`
    - eg: `git+ssh//git@github.com:BozhongFE/bz-login.git`
  - `git+`
    - eg: `git+https://github.com/BozhongFE/bz-login.git`
- tag
  给项目加上一个tag，然后引入项目具体的tag，这是为了防止对项目有了新的改动，不至于影响到业务
  - eg: `git+https://github.com/BozhongFE/bz-login.git#v0.2.0`
