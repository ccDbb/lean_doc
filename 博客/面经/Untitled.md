async function async1(){
    console.log('async1 start')
    await async2()
    console.log('async1 end')
}
async function async2(){
    console.log('async2')
}
console.log('script start')
setTimeout(function(){
    console.log('setTimeout')
},0)  
async1();
new Promise(function(resolve){
    console.log('promise1')
    resolve();
}).then(function(){
    console.log('promise2')
})
console.log('script end')



v-model双向数据绑定



小米的面试题：

写代码和算法题：

1，实现下function.prototype.bind，

2，双向数据链表是什么，将一个数组转为树 ，树转为数组()

3，电话键盘如何实现，给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![image-20201024200941143](/Users/cc/Library/Application Support/typora-user-images/image-20201024200941143.png)

```
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].67
输入："2345678"等
```

4，vue的on emit如何实现的，写代码（完整的观察者模式）

项目上题：

1，js的一些知识点。

2，Watch dep比较卡时怎么处理

