## 块级作用域

MDN 上的官方解释
>In JavaScript, a block is a collection of related statements enclosed in braces ("{}"). For example, you can put a block of statements after an if (condition) block, indicating that the interpreter should run the code inside the block if the condition is true, or skip the whole block if the condition is false.

一言以蔽之：在大括号 "{}" 里面的语句就处在这个大括号构成的块级作用域里。

块级作用域这种特性本身没有问题，但不规范的使用很可能使我们跳入意想不到的坑中，请看下面这段代码：

``` javascript
var me = 100;
if(true){
	var me = 3;
}

console.log(me);
```
猜一猜这个时候 me 打印出来的值是多少？
按理说，for循环这个块级作用域里定义了一个me变量，应该不会影响外层的me，但打印出来的结果是，最外层的me被影响了，变成了3。

为什么？

我个人的理解是这样的： var 定义的变量，虽然在块里面声明，但它的作用域会 ```扩充```到这个块的外面一层，而外层也用一个me变量，这个时候就相当于重复声明，后声明定义的覆盖前面的，所以外层的me就被影响了。

### 问题也就随之而来了

1. 即使我们在外层不使用这个me变量，但它作用域扩充到了外层，在函数执行结束前一直是占着内存的，浪费资源。
2. 如果要在外层使用me变量，但外层me被里面的me覆盖了，值改变了后续肯定会出错，这样一来问题就大发了，不了解块级作用的即使打断点也想不通为啥外层的被改了。

### 解决方案： ES6 let

let声明的变量就在块里，不会扩充到外层，执行结束即销毁，被浏览器垃圾回收机制回收内存，节约资源优化性能，这是优点其一。

其二：既然作用域无法扩充到外层，自然也不会影响外层同名变量，防止了因变量同名带来的相互覆盖而产生的一系列问题，啊！神清气爽~

看下印证一下：
``` javascript
if(true){
	let you = "Chole";
}
console.log(you)	// 报错 ：Uncaught ReferenceError: you is not defined
```



