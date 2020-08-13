# git

## 命令

#### 1. 初始化Git代码库

``` js
$ git init // 初始化
```

#### 2. 查看目录文件

``` js
$ ls -la // 查看目录文件
```

#### 3. 新建文件

``` js
$ touch xxx // 目录下新建文件
```

#### 4. 切换分支

```  js
$ git branch -a // 查看远程分支
$ git branch // 查看本地分支
$ git checkout master // 切换回master分支
```

#### 5. 添加文件

``` js
$ git add [file1] [file2] .. // 添加指定文件到暂存区
$ git add [dir] // 添加指定目录到暂存区，包括子目录
$ git add -A // 添加所有内容
$ git add . // 添加当前目录的所有文件到暂存区，不包括删除的文件
$ git add -u // 添加编辑或删除的文件，不包括新添加的文件
```

#### 6. 查看添加文件

``` js
$ git status -sb // 前面绿色的A，代表已经添加成功了
```

#### 7. 提交

``` js
$ git commit -m "xxx" // 把暂存区的内容正式提交到本地仓库
```

## 解决报错

### 1. 

> fatal: Not a git repository (or any of the parent directories): .git

提示：没有.git目录，解决：

> git init

### 2. 

> Another git process seems to be running in this repository, e.g.  an editor opened by ‘git commit’. Please make sure all processes  are terminated then try again. If it still fails, a git process  may have crashed in this repository earlier:  remove the file manually to continue. 

提示：git被另外一个程序占用

