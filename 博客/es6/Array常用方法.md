## 一、改变数组的操作

### 1、arr.push()

### 2、arr.pop()

### 3、arr.shif()

### 4、arr.unshif()

### 5、arr.splice(start[,[**deleteCount**] [,item……]])

splice删除或者替换已存在的元素或者添加新的元素，*修改了原数组*，返回值为被删除的元素

Array.prototype.splice(start[,[**deleteCount**] [,item……]])

##### start开始修改的元素位置（包含此位置）

##### deleteCount 要删除的元素个数，

如果为0，这表示不删除，如果后边有item代表从此位置前边开始添加元素（如下边例子1）

##### item要添加或者替换的元素，如果是多个，就添加多个值。如果没有此值，只是删除

```
//例子1
let m=[1,2,3,4]
m.splice(0,0,5)
console.log(m)//[5,1,2,3,4]
m.splice(0,2)//删除从0开始的两位
console.log(m) //[2,3,4]

```

### 6、arr.sort([fn])排序

Array.prototype.sort([compareFunction])

返回排序的后数组，改变了原数组。

###### 传入值：对比函数，

对比函数如果不传，则默认时按照Unicode code来排序

返回值：排序后的数组

#### 7，arr.fill(value[, start[, end]])

fill方法改变原数组中从start（默认值从0开始）到end（默认值 array.length）的所有元素。修改了原数组。

##### 参数：

​    value：将要替换的值。（必填）

​     start：开始的数组下标，默认为0（选填）

​       end：结束的数组下表，不包含end标，默认值数组的长度（选填）



```
let m=[1,3,4,5,6]
m.fill('abc',0,2)
console.log(m)//["abc", "abc", 4, 5, 6]
//只传value时，start和end都取默认值。
m.fill("test")
console.log(m)//["test", "test", "test", "test", "test"]
```

#### 8，arr.reverse()

翻转数组，返回的数组时翻转之后的数组，改变了原数组。

### 9，arr.copyWithin(target[,start[,end]])

copyWithin()方法浅复制数组的一部分到同数组的另外一个位置，并返会更好后的数组。不会改变原数组的长度，但是会改变内容。

target从0开始的索引，复制数组的值到该位置。默认值为0，如果为负数，从末尾开始计算

start，从0开始的索引，开始复制元素的起始位置。默认值为0

end，从0开始开始的索引，开始复制元素的结束位置。默认值为数组末尾。



## 二、不改变原数组方法-循环数组

### 1，arry.entries()

返回一个新的Array Iterator迭代器，返回的对象包含数组每个索引的键/值对，返回的迭代器可以用for  of循环迭代器

```
let m=[1,2,3]
for(let [index,value] of m.entries()){
	console.log(item)
}
//0 1
1 2
2 3
```



### 2，arry.keys

返回新的Array Iterator迭代器，返回对象时数组的下标。不改变原数组

```
let m=['a','b','c']
for(let key of m.keys()){
	console.log(key)
}
//0,1,2
```

### 3，arry.



### 2，concat（[value1[, value2[, ...[, valueN]]]]）

链接两个或者更多的数组，不改变原数组，返回连接后的数组

```
const num1 = [1, 2, 3];
const num2 = [4, 5, 6];
const num3 = [7, 8, 9];
const numbers = num1.concat(num2, num3);
console.log(numbers)//[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

value可以不是数组，如果不是数组，会直接在当前数组后边将value加入数组中

```
let m=num1.concat(num2, num3,"0",{a:'b'});
console.log(m)//[1, 2, 3, 4, 5, 6, 7, 8, 9, "0",{a: "b"}]
```

字符串也有此方法

