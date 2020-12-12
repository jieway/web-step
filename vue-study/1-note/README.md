# vue 记事本开发

以下是要实现的功能：

	记事本功能
	1. 新增
		- 生成列表结构（ v-for 数组）
		- 获取用户输入（ v-model ）
		- 回车，新增数据（ v-on.enter )
	2. 删除
		- v-on splice index
	3. 统计
		-v-text
	4. 清空
		-v-on
	5. 隐藏
		-v-show -v-if

此项目参考自该视频,重点是功能实现,没有 CSS 所以点丑😂.

> https://www.bilibili.com/video/BV1HE411e7vY?p=18

## 1.0 基础代码

首先编写 html 页面。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

</body>
</html>
```

引入 vue ，为了避免代码重复，以下内容均在 body 标签中。

```html
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var a = new Vue({
            el: '#app',
            data: {
                message: "Hello world!"
            }
        })
    </script>
```

## 2.0 新增

### 2.1 显示数据

首先要将数据展示出来，采用 v-for 指令来实现数据渲染。

```html
    <div id="app">
        <div v-for="list in lists">
            <span>{{ list }}</span>
        </div>
    </div>

	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var a = new Vue({
            el: '#app',
            data: {
                lists: ["a1","a2","a3","a4","a5","a6"],
                temp: ""
            },
        })
    
    </script>
```

### 2.2 添加数据

首先需要一个文本框，向文本框中添加数据，然后再将数据在渲染出来。

代码如下：

```html
        <input v-model="temp" @keyup.enter="add" placeholder="请输入：">
```

其中 `v-model="temp"` 实现了数据的双向绑定，也就是输入的内容会保存在 temp 变量中，而该变量保存在 data 中。

`@keyup.enter="add"` 则是一个响应，也就是点击键盘 enter 后会触发 add 方法。 @ 本质上是 v-on 指令的简便表示

以下是 js 部分的修改:

```js
        var a = new Vue({
            el: '#app',
            data: {
                lists: ["a1","a2","a3","a4","a5","a6"],
                temp: ""
            },
            methods: {
                add: function(){
                    this.lists.push(this.temp);
                    this.temp = temp;
                }
            }
        })
```

此时就实现了新增功能

## 3.0 删除

### 3.1 设置删除按钮


```html
        <div v-for="(list, index) in lists">
            <span>{{ list }}</span>
            <button @click="remove(index)"> delete</button>
        </div>
```

其中 `@click="remove(index)"` 表示鼠标点击后会触发 remove() 方法, index 则是要删除元素的下标 .

实现对应方法:

```js
                remove: function(index){
                    this.lists.splice(index, 1);
                }
```

## 4.0 统计和清空

统计其实很简单,一个方法就行.

```html
        <div>总数: {{ lists.length }}</div>
```

清空也很简单:

```html
        <button @click="del"> delete all</button>
```

方法实现:

```js
                del: function(){
                    this.lists = [];
                }
```

如果元素为空,那么删除所有的标签将不显示.

添加 v-show 即可,该指令通过修改标签的 display 来实现标签的显示与隐藏.

```html
        <button @click="del" v-show="lists.length != 0"> delete all</button>
```

v-if 也可实现该功能,但是由于直接操作 dom 元素导致消耗过大.

v-if 如下:

```html
        <button @click="del" v-if="lists.length != 0"> delete all</button>
```

## 5.0 总结

没有 CSS 哈,所以比较丑,学习学习.