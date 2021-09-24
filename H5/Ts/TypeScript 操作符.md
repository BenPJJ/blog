# TypeScript 操作符

## 操作符

### 1. keyof 操作符

用于获取某种类型的所有键，并返回类型是联合类型

``` ts
interface Person {
  name: string;
  age: number;
  location: string;
}
type K1 = keyof Person; // 'name' | 'age' | 'location';
type K2 = keyof Person[]; // 'name' | 'age' | 'location' | 'push'
```

### 2. infer

- infer 可以在extends 的条件语句中推断待推断的类型

  ``` ts
  type ReturnType<T> = T extends (...args: any[]) => infer R ? R: any;
  
  type funcReturnType = ReturnType<() => number>
  ```

  



## 特殊操作符

### 1. ! 非空断言操作符

在上下文中当类型检查器无法断定类型时，`后缀表达式操作符!` 可以用于断言操作对象是非 null 和 非undefined 类型

``` ts
# 1. 忽略undefined 和 null 类型
function myFunc(maybeString: string | undefined | null) {
  const onlyString: string = maybeString; // Error
  const ignoreUndefinedAndNull: string = maybeString!; // Ok
}

# 2. 调用函数时忽略undefined 类型
type NumGenerator = () => number;
function myFunc(numGenerator: NumGenerator | undefined) {
  const num1 = numGenerator(); // Error
  const num2 = numGenerator!(); // OK
}

# 3. ! 非空断言操作符会在编译生成的JavaScript 代码中移除，所以切记（变量原意赋值undefined）
const a: number | undefined = undefined;
const b: number = a!;
// 编译后
const a = undefined;
const b = a; // undefined;
```

### 2. ?. 运算符

typescript 3.7 实现了ECMAScript 功能：可选链，`?.运算符` 当遇到null 或undefined 立即停止某些表达式的运行

``` ts
obj?.prop
obj?.[expr]
arr?.[index]
func?.(args)

# 1. 可选属性访问
const val = a?.b;
// 编译后
const val = a === null || a === void 0 ? void 0 : a.b;

# ?. 部分替代 &&
# 切记：
	# 1. && 是专门用于检测false 值，比如：空字符串、0、NaN、null、false
	# 2. 而?. 只会验证对象是否为null 或undefined
if (a && a.b) {} ===> 等价替代 if (a?.b) {}

# 2. 可选元素访问，允许访问非标识符的属性，比如：任意字符串、数字索引、symbol
function tryGetArrayElement<T>(arr?: T[], index: number = 0) {
  return arr?.[];
}
// 编译后
function tryGetArrayElement(arr, index) {
  if (index === void 0) {index = 0};
  return arr === null || arr === void 0 ? void 0 : arr[index];
}
```

### 3. & 运算符

`& 运算符` 可以将现有的多种类型叠加到一起成为一种类型（交叉类型，将多个类型合并为一个类型）

``` ts
type PartialPointX = {x: number};
type Point = PartialPointX & {y: number};
let point: Point = {x: 1, y: 1}

# 同名基本类型属性合并
interface X {
  c: string;
  d: string;
}
interface Y {
  c: number;
  e: string;
}
type XY = X & Y;
type YX = Y & X;
let p: XY = {c: 6, d: 'd', e: 'e'}; // error
let q: YX = {c: 'c', d: 'd', e: 'e'}; // error
// c 的类型会变成never

# 同名非基本类型属性合并
```

### 4. ?? 空值合并运算符

`?? 空值合并运算符` 当左侧操作数为null 或undefined 时，其返回右侧的操作数，否则返回左侧的操作数