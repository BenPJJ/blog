# TypeScript 泛型及应用

## 什么是泛型

在开发过程中，我们不仅要创建一套的定义良好的API，同时也要考虑可重用性。组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型。

（像C#和Java 这样的面对对象语言中）

**失去定义返回类型的能力，同时使编译器失去了类型保护的作用**

## 泛型应用

> 使用泛型条件：
>
> 1. 当函数、接口或类将处理多种数据类型时
> 2. 当函数、接口或类在多个地方使用该数据类型时

### 1. 泛型接口、函数

``` ts
interface Identities<T, U> {
  value: T;
  message: U;
}
function identity<T, U>(value: T, message: U): Identities<T, U> {
  let identities: Identities = {
    value,
    message
  };
  return identities;
}
```

### 2. 泛型类

``` ts
interface GenericInterface<U> {
  value: U;
  getIdentity: () => U
}
class IdentityClass<T> implements GenericInterface<T> {
  value: T;
  constructor(value: T) {
    this.value = value;
  }
  getIdentity(): T{
    return this.value;
  }
}
```

### 3. 泛型约束

- #### 确保属性存在

  有时候，类型变量对应的类型上存在某些属性，这时，除非显式地将特定的属性定义为类型变量，否则编译器不会知道它们的存在。

  **例如：**

  处理字符串、数组时，length属性

  ``` ts
  function Identity<T>(arr: <T>): T {
    console.log(arr.length); // Error
    return arr;
  }
  ===> 改造
  interface Length {
    length: number;
  }
  function Identity<T extends Length>(arr: T): T {
    console.log(arr.length); // 可以获取length属性
    return arr;
  }
  // T extends Length，用于告诉编辑器，支持已经实现Length接口的任何类型，当使用不含有length属性的对象作为参数调用identity 函数时
  ```

- #### 检查对象上的键是否存在

  ``` ts
  enum Difficulty {
    Easy,
    Intermediate,
    Hard
  }
  function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
  }
  let tsInfo = {
    name: "Typescript",
    supersetOf: "Javascript",
    difficulty: Difficulty.Intermediate
  }
  let difficulty: Difficulty = 
    getProperty(tsInfo, 'difficulty'); // OK
  let supersetOf: string = 
    getProperty(tsInfo, 'superset_of'); // Error
  ```

### 4. 泛型参数默认类型

``` ts
interface A<T=string> {
  name: T;
}
```

### 5. 泛型条件类型

根据某些条件（某些条件：类型兼容约束）得到不同的类型

``` ts
interface Dictionary<T = any> {
  [key: string]: T;
}
 
type StrDict = Dictionary<string>

type DictMember<T> = T extends Dictionary<infer V> ? V : never
type StrDictMember = DictMember<StrDict> // string
```

### 6. 泛型工具类型

TypeScript 内置了一些常用的工具类型，比如 Partial、Required、Readonly、Record 和 ReturnType

。。。后期使用到补上

### 7. 使用泛型创建对象

