# TS

## QAS

### interface VS type

**相同点：**

1. 都可以描述一个对象或者函数

   ```js
   # interface
   interface User {
     name: string
     age: number
   }
   interface SetUser {
     (name: string, age: number): void
   }
   # type
   type User {
     name: string
     age: number
   }
   type SetUser = (name: string, age: number): void
   ```

2. 都允许拓展（extends）

   interface 和 type 都可以拓展，并且两者并不是相互独立的，也就是说interface 可以 extends type，type 也可以 extends interface，虽然效果差不多，但是两者语法不同

   ``` js
   # interface extends interface
   interface Name {
     name: string
   }
   interface User extends Name {
     age: number
   }
   # type extends type
   type Name {
     name: string
   }
   type User extends Name {
     age: number
   }
   # interface extends type
   type Name {
     name: string
   }
   interface User extends Name {
     age: number
   }
   # type extends interface
   interface Name {
     name: string
   }
   type User extends Name {
     age: number
   }
   ```

**不同点：**

type 特有：type 可以声明基本类型别名、联合类型、元组等类型

``` js
# 基本类型别名
type Name = string;
# 联合类型
interface Dog {
  wong()
}
interface Cat {
  miao()
}
type Pet = Dog | Cat
# 具体定义数组每个位置的类型
type PetList = [Dog, Pet]
```

interface 特有：interface 能够声明合并

``` js
interface User {
  name: string
  age: number
}
interface User {
  sex: string
}
// User {
//	name: string
//  age: number
// 	sex: string
// }
```

**总结：**

能用 interface 实现，就用 interface，如果不能就用 type