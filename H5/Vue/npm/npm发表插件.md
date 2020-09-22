# npm发表插件
---

### - 注册npm账号
> https://www.npmjs.com/signup

### - 步骤
- 进入插件目录，运行`npm addUser` 或`npm login` ，登录自己的npm用户名、密码和邮箱
- 然后使用`npm whoami` 查看当前用户是不是你的登录的账号
- 发布插件前，在npm 网上查询下有没有相同名称的插件，如果有的话就修改package.json 里面的name 属性
- 然后`npm publish` 就可以把插件上传到npm 网上
- 每次修改后需要修改version 的版本号才能再次发布

### - 总结：

##### + 上传三步走：
``` shell
cd ...
npm login
npm publish
```

#### + 删除：
``` shell
npm unpublish 包名@版本号
```

#### + npm发布规则
- 版本更新小于24小时的包允许下架
- 超过24小时的包的下架需要联系npm维护者
- 如果有npm维护者参与，npm将检查是否有其他包依赖该包，如果有则不允下架
- 如果某个包的所有版本都被移除，npm会上传一个空的占位包，以防后来的使用者不小心引用怀有恶意的替代者
