# class

ES6 引入了Class（类）这个概念，作为对象的模板，通过class 关键字，可以定义类。

## 基本使用

- **Object.assign** 方法可以给动态的增加方法

``` js
Object.assign(xxx.prototype, {
  // ...
})
```

- **ES6 的Class 类是不可枚举的**，ES5 是可以枚举的，不过仅限制在Class 类内部定义的方法
  - **Object.keys()** ，返回一个数组，数组里是该obj 可被枚举的所有属性
  - **Object.hasOwnPropertyNames()** ，返回一个数组，数组里是该obj 上所有的实例属性

``` js
// ES5
function Child() {
  Child.prototype.getName = () => {
    console.log('name');
  };
}
console.log(Object.keys(Child.prototype)); // ["getName"]
console.log(Object.getOwnPropertyNames(Child.prototype)); // ["constructor", "getName"]

// --- 动态添加方法 ---
Object.assign(Child.prototype, {
  setName: () => {
    console.log('setName');
  },
});
console.log(Object.keys(Child.prototype)); // ["getName"， "setName"]
console.log(Object.getOwnPropertyNames(Child.prototype)); // ["constructor", "getName", "setName"]
```

``` js
// ES6
class Child {
  constructor() {
  }

  getName() {
    console.log('name');
  }
}
console.log(Object.keys(Child.prototype)); // []
console.log(Object.getOwnPropertyNames(Child.prototype)); // ["constructor", "getName"]

// --- 动态添加方法 ---
Object.assign(Child.prototype, {
  setName: () => {
    console.log('setName');
  },
});
console.log(Object.keys(Child.prototype)); // ["setName"]
console.log(Object.getOwnPropertyNames(Child.prototype)); // ["constructor", "getName", "setName"]
```

- ES6 中，类的属性名可以使用表达式

``` js
let methodHame = 'getName';
class Child {
  constructor() {
  }

  [methodName]() {
    console.log('name');
  }
}
```

- **class 不存在变量提升**
- **super**

``` js
class Child {
  constructor(name) {
    this.name = name;
  }

  getName() {
    console.log('name');
  }
}

class child extends Child {
  constructor(name, age) {
    super(name);
    this.age = age;
  }
  
  getName() {
    super.getName();
    console.log(this.age);
  }
}
```

## 私有方法

ES6 不提供私有方法，只能通过变通方法模拟实现

- 一种是在命名上加以区别，在方法前面加上**_（下划线）** ，表示这是一个只限于内部使用的私用方法；但是，这种命名是不保险的，在类的外部，还是可以调用到这个方法

``` js
class Child {
  constructor() {
  }

  getName() {
    console.log('name');
  }
  
  _setName() {
    console.log('setName');
  }
}
```

- 一种是索性将私有方法移出模块，因为模块内部的所有方法都是对外可见的

``` js
const setName = () => {
	console.log('setName');
}

class Child {
  constructor() {
  }

  getName() {
    setName();
  }
}
```

- 另一种是利用Symbol 值的唯一性，将私有方法的名字命名为一个Symbol 值

``` js
const methodName = Symbol('getName');

class Child {
  constructor() {
  }

 	[methodName]() {
    console.log('name');
  }
}
```

## 静态方法

- 方法不会被实例继承，而是直接通过类来调用，这就称为静态方法

``` js
// StaticMethod.js 
export dafault class StaticMethod {
  static getCommon() {
    console.log('子类的静态方法');
  }
}

StaticMethod.getCommon();
```

- 静态方法只能在静态方法中调用，不能在实例方法中调用

``` js
// StaticMethodParent.js
export default class StaticMethodParent {
  static getCommon() {
    console.log('父类的静态方法');
  }
}

class StaticMethod extends StaticMethodParent {
  static getCommon() {
    super.getCommon();
  }
}
```

### 为什么使用静态方法

- **阻止方法被实例继承**，
- **类的内部相当于实例的原型** ，所有在类中直接定义的方法相当于在原型上定义方法，都会被类的实例继承。
- 静态方法可以被子类继承，也可以被super 调用
- **静态方法中this 指向** ，this 指向类而不是类的实例





