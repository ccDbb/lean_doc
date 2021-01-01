### Promise常用方法

promise是以同步的代码实现异步回调，解决了之前异步只能层层嵌套回调模式。promise也有些缺点，一旦开始无法取消promise回调。

#### 1，基本使用

##### 1）获取promise对象。

```
let m=new Promise((resolve,reject)=>{
	resolve(2)
});
m.then(value=>{
console.log(value)//2
},error=>{
//reject时的处理在这里
})
```

a，promise时v8引擎内部实现的一个对象，我们用的时候可以使用new操作符来得到一个promise对象。如上诉代码。

b，另外我们可以直接调用Promise.resover(2)来获取一个promise对象。如下

```
let m=Promise.resolve(function(){return 2})//这里resolve里可以传入函数或则变量
m.then(value=>{
console.log(value)//2
},error=>{
//reject时的处理在这里
})
```

c，还可以调用promise对象的其它方法来生成promise

##### 2）执行

当我们执行new Promise时，会直接执行new Promise括号里里的函数内容，直到function内容结束或者return；resolve并不会阻断代码执行，只是返回一个值，之后then可以接收这个值。

生成promise后，不管有没有显示调用resolve或者rejeact都会返回一个promise，then函数里也是会返回一个promise，所以，一个promise时可以一直链式调用下去，不会结束。

#### 2，常用方法

promise.all怎么用

Promise.race()和promise.all()区别

#### 3，和async、await区别优缺点

async、awatie具体用法可以查看对应章节的内容，此处只分析和promise的区别。

promise缺点：多层嵌套时书写方式会充满了then方法。async代码风格更接近同步。

优点：在同时发生多个异步请求时，可以直接用promise.all来实现。async无法实现。

#### 4，如何打断promise的下一步执行then或者catch呢?

我们知道promise可以一直.then().then()执行下去，但是我们希望在其中一个then里某些条件下，不继续执行下边then()，也不执行catch()。

我们知道promise是一旦执行就无法取消，而它有resolve，reject、pending三种状态。所以如果想中间不往下执行，可以把它设置为pending状态。这种取巧的方式。

```

```





