### map用法

### 一，定义、初始化map

#### 构造函数生成map

map是v8解析器里内置的一个对象，所以我们在初始化的时候，可以直接使用构造函数。

```
let map=new Map();
```

#### 赋值

map赋值有两种方式，一种是直接用map自带的set方法来设置，一种是初始化时，直接在构造函数中传入。

#### (1）直接set方法

```
map.set("key","1");
map.get("key");//"1"

```

##### a，map的key值可以是字符串或者数字，但是1和'1'并不是同一个key。

```
map.set("1","test1")
map.get("1")//"test1"
map.get(1)//undefined

let let m="",n=false;
map.set(m,"m1")
map.get(m)//m1
map.get(n)//undefined
```

set的key只有严格相等，才属于同一个key，比如字符串“1”和数字1虽然用==比较是相同的，但是===比较是false，不是同一个key。

只有通过严格比较===是相同的，才属于同一个key。

##### b，map的key值可以是boolean

```
map.set(true,"true1");
map.set({a})
```

##### c，map的key值可以是对象

如果是对象，要注意，这里set对象时，map里保存的是这个对象的引用地址，所以，a={a:1};b={a:1};此时map.set(a)是无法通过map.get(b)来获取的

```
let a={a:1},b={a:1};
map.set(a,222);
map.get(b)//undefined,a和b值一样，但是引用地址不同，所以属于不同的key值
map.get(a)//222
let c=a;
map.get(c)//222
```

如上代码，只有对象的引用地址一致，key值才是相等的。也可以通过和字符串一样通过严格比较===相等的，才属于同一个key。

##### d，map的key可以是函数。

当mapkey值是函数时，如果函数是执行的，那么key值是这个函数里的返回值，如果没有设置返回值，那么默认为undefined。如果函数没有执行，key为这个函数本身

```
function fn1(){
	console.log(2);
}
function fn2(){
	return 23
}
map.set(fn1,"fn1");//fn1函数的内容=>fn1
map.set(fn1(),"fn1-1");//undefined=>fn1-1
map.set(fn2(),"fn2");//23=>fn2
```



#### (2）以数组作为参数传入构造函数

```
let map=new Map([['key1','1'],['key2','2']]);
map.get('key1')//1
map.get('key2')//2
```

map构造函数接受数组作为参数时，实际执行的如下操作

```
let map=new Map();
let str=[['key1','1'],['key2','2']];
str.forEach(([key,value])=>{
	map.set(key,value)
})
```

从上诉代码可以看出，构造函数传入数组时，传入的值：

a，必须是二位数组，一维数组时会报错。

```
VM97:1 Uncaught TypeError: Iterator value k2 is not an entry object
    at new Map (<anonymous>)
    at <anonymous>:1:5
```

因为forEach第一层循环之后，调用之前函数([key,value])参数必须是可以遍历的iterator。如果是一维数组就会报错。

b，如果二维数组最里层数组长度大于2，那么后边的值会被忽略，只取前两位

```
let map=new Map([['key1','1',2,4],['key2','2']]);
map//{"key1" => "1", "key2" => "2"}
```

c，如果传入的是对象，不会报错，但也不能正常赋值。只会默认赋值为undifened（这个问题我也没有搞清楚为什么。搞清楚了再来补充。下边代码是浏览器执行结果）

```
let map=new Map([{"key":2}]);
map//{undefined => undefined} 
```

map的key值可以是任意类型的变量，这是它优于对象的一点。

map里不会有重复元素。如果在使用set时，如果值已经存在，则会覆盖此值。

### 二、map常用属性

#### map.size返回map成员数

```
let map=new Map([['name','cc']])
map.size //1
```



### 三、map常用方法

#### 1、map.get(key)

返回对象的value

```
let map=new Map([['name','cc']])
map.get('name');//cc
```

如果key值不存在，返回undefined

```
map.get('age');//undefined 
```

#### 2、map.set(key,value)

在第一部分初始化map时已经详细讲过了。添加一对值到map里。如果key已经存在，会覆盖以前值。

返回值undefined

#### 3、map.has(key);

has方法返回一个布尔值，判断key是否存在map中

```
map.has('age')//false;
map.has('name')//true
```

#### 4、map.delete(key)

delete删除某个键，如果删除成功返回true，如果失败返回false;

如果删除一个不存在的key时，返回false，并不会报错。

```
map.delete('age')//false;
map.delete('name')//true
```

#### 5、map.clear()

clear清楚所有成员，没有返回值（其实是undefined）；

```
map.set("name","cc2");
map.size;//1
map.clear();
map.size;//0
```

#### 6、map.keys()

keys()返回map里包含所有的键名遍历器，可以直接用for of来循环得到。

这里map.keys()返回的并不是数组。

```
let map=new Map([
['name','cc'],
['age','118']
])
let keyList=map.keys()
console.log(keyList) //MapIterator {"name", "age"}
for(let key of keyList){
	console.log(key)
	    //name 
  	 //age
}
```

#### 7、map.values()

values()返回map里所有值的遍历器。用法和map.key()一样

#### 8、map.entries()

entries()返回map里所有成员的遍历器，包含key、values

```
for(let item of map.entries()){
	console.log(item)//
}
//["name", "cc"]
 //["age", "118"]
```

可以用结构函数直接取到key，value

```
for(let [key,value] of map.entries()){
	console.log(key,value)
}
//name cc
//age 118
```

map默认的遍历器是entries，所以遍历map.entries()和遍历map一样的

```
for(let [key,value] of map){
	console.log(key,value)
}
//name cc
//age 118
```

#### 9、map.forEach()

循环获取map里值，回调方法有三个参数，依次是：value、key、entrie，其中entrie为key value对象。

```
map.forEach((value,key,entrie)=>{
	console.log(value,key,entrie)
})
//cc name Map(2) {"name" => "cc", "age" => "118"}
//118 age Map(2) {"name" => "cc", "age" => "118"}

```

map的取得顺序就是放入的顺序。

### 四、map与其他数据结构相互转换

#### 1、map转为数组

利用结构函数[...map]

```
let map=new Map([
  ['name','cc'],
  ['age','118']
])
[...map] //[Array(2), Array(2)]
```

利用for循环，添加到数组中。

```
let arr=[];
for(let item of map){
arr.push(item)
}
```

#### 2，数组转为map

直接传入构造函数中

```
let str=[
  ['name','cc'],
  ['age','118']
]
let map=new Map(str);
```

#### 3，map转为对象

使用for循环，如果key值是普通字符串，可以如下转。

```
let obj={};
for(let [key,value] of map){
	obj[key]=value;
}
console.log(obj)
//{name: "cc", age: "118"}
```

如果key是对象或者函数，默认时会调用tosString方法，将key转为字符串。如果想无损转换，需要自行处理下key的值。

#### 4，对象转为map

a、使用for循环，对象默认没有遍历器，所以不能使用for of，可以使用for in

```
let obj={name: "cc", age: "118"};
for(let key in obj){
	map.set(key,obj[key])
}
map//

```

b、直接使用Object.entries(obj)，将obj转化为数组，之后使用数组转为map方式

```
let map=new Map(Object.entries(obj))
map//
[["name", "cc"],
["age", "118"]]
```

c、使用Object.keys(obj)获取对象key的遍历器

```
let obj={name: "cc", age: "118"};
for(let item of Object.keys(obj)){
	map.set(item,obj[item]);
}
```

#### 



