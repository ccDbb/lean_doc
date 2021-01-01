### string (字符串类型)  可通过typeof m=='string'来检测

### number（数值类型）可通过typeof m == ’number‘ 来检测

### Boolean （布尔类型）可通过typeof m== ’ boolean‘ 来检测

### undefined （未定义）

可通过typeof m =='undefined'

在if里进行判断时，undefined为false。



### null (空值)

### symbol

### object（对象）

## 判断类型，

对于基础类型，可以用typeof来判断

对于引用类型，或者null，可以用tosting来判断Object.prototype.toSting.call( m );

对于基础引用类型，可以用instanceof来判断,