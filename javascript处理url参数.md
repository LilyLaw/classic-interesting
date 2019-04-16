## JavaScript 处理url参数

## 要求
将url中的参数组合成键值对的方式

### 实现
1. 方法一：字符串函数处理

``` javascript
function queryUrlParams(url){
	let getparams = url.split('?');		// 获取参数串
	let getEpa = getparams[1].split('&');
	let gatherParams = {};
	getEpa.map((item,i)=>{
		let tmp = item.split('=');
		gatherParams[tmp[0]] = tmp[1];
	});
	console.log(gatherParams)	// 所得最终结果
}
```
总结：这种方法完全ok，


2. 方法二： 正则表达式

``` javascript
function queryUrlParams(url){
	let reg = /([^?=&]+)=([^?=&])/g,	// 编写正则
		obj = {};
	url.replace(reg,function(){
		obj[arguments[1]] = arguments[2];
	});
	console.log(obj);	// 所得最终结果
}
```


### 总结
这两种方法完全ok，但相比较起来还是有些差距：
（1）从最直观的代码量上看，第二种方法明显代码更少，更简洁，更直接。
（2）从执行效率上说，正则表达式直接匹配，如果表达式书写规范高效的话，代码性能更高节省资源。

同时，也应该意识到，正则表达式的可读性较差，一旦写错，将会大量消耗内存资源，学习成本较高。

推荐使用第二种方法，毕竟优越的性能值得我们去学习。

### 拓展

开发过程中，如果需要经常处理url，则可以将该函数扩展到原型链，这样每一个string都可以直接调用该方法，而不再使用传参的方式。

``` javascript
// 扩展
String.prototype.lllQueryUrlParams = function(){
	let reg = /([^?=&]+)=([^&?=])/g,	// 编写正则
		obj = {};
	this.replace(reg,(...arg)=>{	// es6 语法去自行学习。
		obj[arg[1]] = arg[2];
	});
	console.log(obj);
}

// 调用
let mystring = 'https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=git%20%E4%BF%AE%E6%94%B9repository%20%E7%9A%84%E5%90%8D%E5%AD%97&oq=%25E9%2587%2591%25E8%259E%258D%25E5%25AD%25A6%2520%25E9%25BB%2584%25E8%25BE%25BE%2520%25E7%2599%25BE%25E5%25BA%25A6%25E4%25BA%2591&rsv_pq=c4d80db3000127a8&rsv_t=a089WiZoQJJfeoZG%2FdLIhjO3O4%2BdthUsY32GSMHv5WIfFDjhEtMcSidpYac&rqlang=cn&rsv_enter=1&rsv_sug3=39&rsv_sug1=27&rsv_sug7=100&rsv_sug2=0&inputT=12327&rsv_sug4=12327';
mystring.lllQueryUrlParams();
```

关于正则表达式和es6语法自行去学习