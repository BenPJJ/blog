# React Hook

## Hook

> React Hook 是React16.8 的新增特性，React Hook 就是一些React 提供的内置函数，这些函数可以让Function Component 和Class Component 一样能够拥有组件状态（state）以及进行副作用（side effect）

### 1. 为什么使用hook（可以解决什么问题）

1. Component 非UI 逻辑复用困难
2. 组件的生命周期函数不适合side effect 逻辑的管理
   - 相互关联的逻辑被分散到不同的函数中会导致bug 的发生和产生数据不一致的情况（componentDidMount、componentDidUpdate、componentWillUnmount）
   - 在组件的同一个生命周期函数放置很多互不关联的side effect 逻辑，导致组件逐渐变得难以测试
   - 而Hook 可以将和某个side effect 相关的逻辑都放在同一个函数里面，还可以实现被不同的组件进行复用
3. 不友好的Class  Component

**使用react hooks的好处：**

1. react hooks 的出现提供了更好的模块化代码的方式，抽离公共的UI的时候，可以变为更小粒度的拆分
2. reack hooks 能够大大的减少我们的大代码量，不需要再去理解复杂的class Component，一切都变的更加简单
3. 切记：Function Component 始终是函数，只要re-render，里面的代码都会重新执行，内联函数、内联对象都会被重新创建

**高阶组件、renderProps的缺点：**

1. 高阶组件的开发对开发者不友好
   - 新人开发需要花费时间搞懂和适应写法
2. 高阶组件之间组合性差
   - 要为组件添加不同的功能，需要为同一个组件嵌套多个高阶组件，prop可能容易丢失或者被覆盖

3. 容易发生wrapper hell，即组件嵌套

**Hook VS 高阶组件、renderProps：**

1. 写法简单
   - 每个Hook 都是一个函数，因此写法简单，开发者更容易理解

2. 组合简单
   - Hook 组合起来简单，组合只需要同时使用多个hook 就可以使用到所有的功能

3. 容易扩展
   - Hook 具有很高的可扩展性，可以通过自定义Hook 来扩展某个Hook 的功能

4. 没有wrapper hell
   - Hook 不会改变组件的层级结构，也就不会有wrapper hell 问题的产生

---

### 2. hook使用

---

#### **useState**

---

1. Function Component 存在的问题：

   Function Component（无状态组件） 每次执行的时候都会生成新的函数作用域，所以同一个组件的不同渲染之间**不能够共用状态**的

2. useState 解决问题：

   useState 允许Function Component 将自己的**状态持久化**到React 运行时（runtime）的某个地方（memory cell）,这样在组件每次重新渲染的时候就可以从这个地方拿到该状态，而且当该状态被更新的时候，组件也会重渲染

   ``` jsx
   # initialState 参数只会在组件的初始渲染中起作用，后续渲染时会被忽略
   const [state, setState] = useState(initialState);
   
   # 如果state 需要通过复杂计算，则可以传入一个函数
   const [state, setState] = useState(() => {
     const initialState = someExpensiveComputation(props);
     return initialState; 
   });
   ```

---

#### useEffect

---

1. 基本用法：

   > useEffect(fn, [deps])

   useEffect 接受的函数会在**reader 之后执行**，函数执行后，如果返回一个函数，那么返回的函数会在执行下一个effect 之前（即上一个effect）销毁

   ``` jsx
   console.log('start');
   const [count, setCount] = useState(0);
   useEffect(() => {
     console.log('log on effect', count);
     return () => {
       console.log('log on effect return fn', count);
     }
   }, [count])
   console.log('render');
   return (
     <div className="App">
     	<h1>{count}</h1>
       <h2 onClick={() => setCount(count + 1)}>Add Count</h2>
     </div>
   )
   
   // 打印顺序
   // start \ render \ log on effect 0
   // 点击 Add Count 触发 count 更新，打印顺序
   // start \ render \ log on effect return fn 0 \ log on effect 1
   ```

2. **切记：**

   - 在Fn 中使用到的变量需要传入到deps，否则会出现取不到最新的值问题
   - 传入deps 的值，不要传递函数中的方法，否则会造成死循环

   ``` jsx
   # 这样会造成死循环，因为每一次重新 render handle 就会被重新创建，useEffect 每次都会检测到变化
   function App() {
     const [count, setCount] = useState(0);
     const handle = () => { setCount(count + 1) };
     useEffect(() => {
       handle();
     }, [handle])
   }
   ```

---

#### useLayoutEffect

---

会在所有的DOM 变更之后**同步**调用effect，在浏览器执行绘制之前，useLayoutEffect 内部的更新计划将被同步刷新

1. 应用场景
   - 可以读取DOM 布局并同步触发重渲染；

---

#### useEffect VS useLayoutEffect

---

1. 相同点
   - 都会在所有的DOM 变更之后调用effect
2. 异同点
   - useLayoutEffect 是同步调用，会阻塞视觉更新
   - useEffect 是异步调用，不会block browser painting（阻止浏览器绘画）

---

#### useCallback

---

1. 基本用法

   > useCallback(fn, [deps])

2. 解决什么问题，也是为什么有这个hooks的原因

   组件更新的时候，组件内的内联函数都会被重新创建，如果将这个**内联函数变成依赖**，或者**传递给某个子组件**，都会导致一些性能问题

   ``` jsx
   function App() {
     const handle = () => {}
     // const handle = useCallback(fn, [deps])
     return (
     	<div className="App">
         <Cildren onClick={handle} />
       </div>
     )
   }
   ```

3. 优点

   - 不会每次重新声明新的函数，避免释放内存、分配内存的计算资源浪费

   - 子组件不会因为这个函数的变动重新渲染（和React.memo 搭配使用）

---

#### useMemo

------

1. 基本用法

   > useMemo(() => fn, deps)

   useMemo 的回调函数会在**渲染期间执行**

2. 应用场景

   - 需要复杂计算的时候，可以用来**存储**

   - 用useMemo 来**优化**引用数据的传递

     ``` jsx
     # 存储复杂的计算
     const value = useMemo(() => computeExpensiveValue(a), [a])
     
     # 优化引用数据的传递
     const childrenStyle = useMemo(() => ({ height }), [height])
     ```

---

#### useCallback VS useMemo

---

1. 相同点：

   useMemo 和 useCallback 都会在组件第一次渲染的时候执行，之后会在其依赖的变量发生改变时再次执行

2. 不同点：

   并且这两个hooks 都返回**缓存的值**，useMemo 返回**缓存的变量**，useCallback 返回**缓存的函数**

3. **切记：**

   不是所有的变量或函数都需要使用useMemo、useCallback，只有哪些确实有需要被缓存的才使用

---

#### useRef

---

1. 基本用法

   useRef 返回一个可变的ref 对象，其`current` 属性被初始化为传入的参数（initialValue），返回的ref 对象在组件的整个生命周期内保持不变

   为什么不能直接使用ref，非得使用ref.current？

   因为为了保存多次useRef 是同一个值，只有对象引用才能做到

2. 应用场景

   - 用来**访问dom 节点**，或者访问一堆列表的节点

     ``` jsx
     const ref = useRef(null)
     const listRef = useRef([])
     <div ref={ref}></div>
     {
       arr.map((num, index) => {
         return (
           <div key={num} ref={(_ref) => listRef.current[index] = _ref}></div>
         )
       })
     }
     ```

   - ref 是**不能被监听**

     ``` jsx
     useEffect(() => {
       console.log(ref)
     }, [ref])
     ```

   - 用来**存储**一些不用引起re-render ，但是需要变化的变量

     ``` jsx
     const [count, setCount] = useState(0);
     const countRef = useRef(null);
     useEffect(() => {
       countRef.current = count;
     })
     ```

   - 定时器

     ``` jsx
     const [timer, setTimer] = useState(0);
     const intervalRef = useRef();
     useEffect(() => {
       intervalRef.current = setInterval(() => {
       	setTimer(1);
       }, 1000);
         
       return () => {
          clearInterval(intervalRef.current);
       }
     }, [timer])
     ```

3. 经典例子

   ``` jsx
   # alert 弹出的不是count 的实时状态，React 会重新渲染组件，每一次渲染都会拿到独立的count 状态，并重新渲染一个handelAlertClick 函数，每一个handleAlertClick 里面都有它自己的count
   const [count, setCount] = useState(0);
   function handleAlertClick() {
     setTimeout(() => {
       alert('You clicked on: ' + count);
     }, 3000);
   }
   <p>You clicked {count} times</p>
   <button onClick={() => setCount(count + 1)}>Click me</button>
   <button onClick={handleAlertClick}>Show alert</button>
   ===> 改造后
   const [count, setCount] = useState(0);
   const countRef = useRef();
   useEffect(() => {
     countRef.current = count;
   })
   function handleAlertClick() {
     setTimeout(() => {
       alert('You clicked on: ' + countRef.count);
     }, 3000);
   }
   ```

---

#### useRef VS createRef

---

1. 不同点
   - useRef 像一个变量，类似与this
   - createRef 每次渲染都会返回一个新的引用，而useRef 每次都会返回相同的引用

---

#### useImperativeHandle

---

useImperativeHandle 提供了一个类似实例的东西，通过useImperativeHandle 的第2个参数，所返回的**对象的内容挂载到父组件的ref.current** 上

``` jsx
const Children = forwardRef((props, ref) => {
  const inputRef = useRef(null);
  useImperativeHandle(ref, () => {
    name: '子组件暴露给父组件的name属性',
   	focus: () => {
      inputRef.current && inputRef.current.focus();
    }
  })
    
  return (
  	<>
      <input type="text" ref={inputRef} />
    </>
  )
})

const Parent = () => {
  const ref = useRef(null);
  return (
  	<>
   	  <Children ref={ref}/>
      <button onClick={() => {console.log(ref.current)}}>获取子组件暴露给父组件的东西</button>
    </>
  )
}
```

#### forwardRef

函数式组件不能直接使用ref

``` jsx
const ref = useRef(null)
const app = (
  <div>
  	<Button ref={ref} />
  </div>
)

const Button = （props）=> {
  return <button></button>
}

const Button = React.forwardRef(props, ref)=> {
  return <button></button>
}
```

#### useContext

**现象：**

React 中组件之间传递参数的方式是props，假如**父组件**中定义了**某个状态**，而这些状态需要在该组件**深层次嵌套的子组件**中被使用的话，就需要将这个状态以props 的形式层层传递，这就**造成了props drilling**的问题

**作用：**

实现跨组件层级直接传递变量，实现共享

``` jsx
# 1. 创建上下文
const CountContext = createContext();

function Counter() {
  # 3. 使用上下文
  const count = useContenxt(CountContext);
  return (
  	<h2>{count}</h2>
  )
}

function Example() {
  const [count, setCount] = useState(0)
  return (
  	<div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>click me</button>
      # 2. 圈定作用域
      <CountContext.Provider value={count}>
      	<Counter />   
       </CountContext.Provider>
    </div>
  )
}
```

#### useReducer

#### useDebugValue

需要了解的：

> Object.is
>
> Object.defineProperty







