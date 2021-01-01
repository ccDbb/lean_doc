## 一、字符串中对码点的操作

js中所有的文字和命令都是由码点组成，unicode规定了代码点对应的字符（比如"97"对应的字符是"a"），但是没有定义怎么存储。

unicode的不同实现，用了不同的存储方式，UTF-8、UTF-16、UTF-32不同的实现。

js里默认以UTF-16来存储码点，也就是两个字节（16位）对应一个字符。

### 1，String.fromCharCode()

String.fromCharCode()是一个String类上的静态方法。

输入：码点(10进制或者十六进制码点)

返回字符码对应的字符

（这里都是以UTF-16编码的字符）

```
console.log(String.fromCharCode(98)) //b
console.log(String.fromCharCode(65)) //A
console.log(String.fromCharCode(65,95,78,65,95,78))//A_NA_N
String.fromCharCode(0x404);//Є
```

### 2，String.fromCodePoint(); 

此方法和formCharCode用法一样，唯一区别是当String.fromCharCode不能返回补充字符对应的值（i.e. code points `0x010000` – `0x10FFFF`）。

但是fromCodePoint可以返回四个字节补充字符如下

```
console.log(String.fromCodePoint(0x2F804));//"你"
console.log(String.fromCharCode(0x2F804));//不知道怎么打出来，请自行在浏览器测试
```

下面试官网原文对这两个方法对比的的描述

> [`String.fromCharCode()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode) cannot return supplementary characters (i.e. code points `0x010000` – `0x10FFFF`) by specifying their code point. Instead, it requires the UTF-16 surrogate pair in order to return a supplementary character:

### 3，String.prototype.charCodeAt()

charCodeAt()是字符串对象的方法，

输入：是字符串中某个字符的所在的索引(从0开始)。

返回值：此索引对应的字符的码点（以介于0-65535中间的整数来表示的）

拿一个官方例子

```
const sentence = 'The quick brown fox jumps over the lazy dog.';

const index = 4;

console.log(`The character code ${sentence.charCodeAt(index)} is equal to ${sentence.charAt(index)}`);
// "The character code 113 is equal to q"

```

上诉例子sentence.charCodeAt(index)返回的是字符串sentence索引为4的位置的字符，也就是'q'所对应的码点113(可以用String.fromCharCode(113)来验证)。

### 4，String.prototype.charAt()

charAt()是字符串对象上的方法。

输入：字符串中某个字符的索引（比如第四个字符，输入3，从0开始）

输出：此索引对应的字符

```
const sentence = 'testcc';

const index = 4;

console.log(` ${sentence.charAt(index)}`);
// c
console.log(sentence.chartAt())//t 
```

如果输入的index超出了当前字符串的长度，则返回空字符串“”

如果不输入index则默认传入的参数是0，返回字符串第一个字符

### 5，String.prototupe.codePointAt()

感觉这个方法和String.prototype.charCodeAt()一样的作用，用法也一样，唯一区别是传入一个大于字符串长度的index时返回值，一个是undefined一个是NAN。



### 二、常用方法

#### 1，concat（[value1[, value2[, ...[, valueN]]]]）

链接两个字符串，数组也有此方法。

### 