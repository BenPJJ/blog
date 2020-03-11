# path
---
### - API
- path.basename(path[, ext])
`path.basename()` 返回`path`的最后一部分
  - param
    > path *string*
    > ext 可选的文件扩展名 *string*
  - return
    > *string*
  - eg
    ``` js
    path.basename('./modules/home/index.js')
    // return 'index.js'

    path.basename('./modules/home/index.js', '.js')
    // return 'index'
    ```
