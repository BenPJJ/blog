# js跳出循环

跳出循环有三种方法：break、continue、return

## break

用来终止循环、让循环不再往下继续

``` js
for (let i = 0; i < 5; i += 1) {
  console.log(i); // 0 1 2 3
  if (i === 3) break;
}
```

## continue

用来跳过循环，继续往下循环

``` js
for (let i = 0; i < 5; i += 1) {
  if (i === 3) continue;
  console.log(i); // 0 1 2 4
}
```

## return

`return` 只能出现在函数里，如果出现在上面实例里的`for` 循环里就会报错，`return` 出现在函数里的作用就是即使下面还有内容也不再继续往下执行了

