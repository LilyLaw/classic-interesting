## css 水平垂直居中

### 水平居中

1. 最简单的 ```margin:auto;```
	``` html
	<style>
        body{
            height: 100%;
            background: lightgreen;
        }
        .block{
            width: 200px;
            background: green;
            color: #fff;

            margin: auto;   /* 此处设置居中 */
        }
        .inline{
            margin: auto;
        }
    </style>
    <div class="block">这是要居中的块状元素</div>
    <span class="inline">这是要居中的内联元素</span>
	```
	**注意** 此种方式设置的居中，(1). 如果被居中元素是块状元素，必须给要元素一个宽度，否则占满一整行看不到居中效果；(2). 内联元素使用margin:auto 无法实现居中，因为```width```,```height```,```margin```,```padding``` 对内联元素不起作用
	
2. flex 布局
	``` html
	<style>
        .block{
            background: green;
            height: 300px;

            /*此处开始设置居中*/
            display: flex;
            justify-content: center;
        }
        .con{
            color: #fff;
            background: red;
        }
    </style>
    <div class="block">
        <div class="con">这是要居中的块状元素</div>
    </div>
	```
	给需要居中的元素的**父元素**设置flex布局，且```justify-content:center;``` 
	
3. 