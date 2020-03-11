# import * as xxx from 'xxx'作用
---
### - 作用
- `import * as xxx from 'xxx'`会将 "xxx" 中所有 export 导出的内容组合成一个对象返回(或`import * as obj from 'xx'` 这种写法是把所有的输出包裹到obj对象里);
``` js
export const msg = state => state.msg
```
``` js
import * as getters from './getters'
```
### - 比较
- `import * as xxx from 'xxx'`会将若干export导出的内容组合成一个对象返回
- `import xxx from 'xxx'`只会导出这个默认的对象作为一个对象
