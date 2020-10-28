小米面试题

1，vue和react区别，为什么选vue

2，webpack只引入组件一部分，或者叫去除多余内容

3，promise相关的执行顺序和reject触发

4，节流和抖动区别，如何实现。

防抖是n时间段内只执行一次，如果在n内清楚计数器，从新计算。

例如监控浏览器滚动条事件时

```
function showTop(){//获取滚动条距离顶部距离
	let top=document.body.scrollTop ||document.documentElement.scrollTop;
	console.log('top='+top)
}
//节流实现代码
//生成timer,n毫米后第一次调用方法。
//如果ns内再次执行此回调，清楚上次timer，重新设置timer，
//调用方法
//
function deplayfn(fn,wait){
	let timer=null; 
	return ()=>{
		if(timer){clearTimeoou(timer)}
		timer=setTimeout(fn,wait)
	}
}
window.onscroll=deplay(showTop,1000)

```

节流每隔n时间段内只执行一次，可以用settimeout或者时间戳来实现。

5，vue虚拟树,

6, 自己封装一个事件上的通用方法，比如@click.trim

7，项目中遇到比较难得事情是什么，如何解决的





#### 京东面试题（2面）

1，vuex都有什么属性

2，vuex实现v-model的实时修改

3，单点登录的机制，token和session的区别。

4，xxs攻击，和csrf攻击，如何解决。

5，算法题：数组中有重复元素，查找那个元素重复次数最多。

6.，算法题：10000ms转为hour、min、second，只用加减乘除，不许用现有方法和位运算

7，div点击当前元素显示，点击div之外的隐藏。

8，webpack loader和plugin区别是什么

##### 9，如何在一行显示两个div，一个固定不变，一个跟随父变化

变化的元素设置为flex:1，不变的设置为flex:0



v-model

provide/inject 组件间通信



京东面试：

1，有自己写过loadder或者plugin组件没有

2，webscot头信息如何建立长连接的

3，webstorm和gulp区别，了解gulp流的概念吗？

4，跨域解决方案 postmessage。

5，强缓存和协商缓存

6，页面优化都有哪些

7，eventLoop  事件循环

8，async和awit原理， 携程的概念

9，模块的理解，Amd es6 commonjs区别。

10，new操作符都做了什么。



#### 自己整理的答案：

6，页面优化都有哪些



我们经常关注的页面优化分加载阶段和交互阶段

加载阶段：

1，使用浏览器缓存，浏览器缓存分为强缓存和协商缓存，q

##### 10，new操作符都做了什么。

```
function fn(){
	this.m=0;
}
```

主要做了以下四步

```
1. var obj=new Object();
2. obj.__proto__=fn.prototype
3. fn.call(obj)
4. return obj
```



腾讯面试

1，性能优化  

2，http缓存，强缓存/协商缓存

3，node异步高并发的问题

4，cros简单请求和复杂请求的区别

5，vue的原理

6，vue-router的history的原理

7，跨域的问题



















13581701532

yonyou@1988



