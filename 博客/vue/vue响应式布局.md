面试中vue一个必问的知识点就是vue的双向数据绑定原理。用法大家都懂，只是有时候说起来总是逻辑不清晰，这篇文章是以我理解的角度来解释这个原理。

vue双向数据绑定可以分为四个部分

### 1，vue中data数据变为可观测

在new vue()时，会循环遍历data中所有对象的属性，都变为可观测性。

如果是对象就通过object.propotype方法将每个属性添加get、set方法。这样每次访问属性或者修改属性时都会触发get或者set方法。

如果是数组，会监控会引起数组变化的方法（push、pop、shift、unshift、splice、reverse、sort），进行拦截，这样每次修改数组时也会触发对象的方法。

接下来的几部分都是以对象的get、set为例。

### 2，vue中watch对象可以看成是数据变化时需要更新的dom（真实的是watch会通知真实dom的修改）。

watch对象中做的事情：

   1.调用对应属性，触发属性的get方法。2，把watch本身赋值给window.target对象。

### 3，属性的get、set函数的实现

get的实现：第一步中拦截的属性的get方法的内部也会进行两步操作，1，是调用Dep.deppend方法，这个方法，会把window.target（这个对应的值为第二步中被赋值的watch的值）放入一个数组里，这个数组时就是保存的对象所依赖的所有watch。2，返回属性对应的值。

set的实现：1，设置值，2，调用dep.updata方法，这个方法会遍历dep中数组的watch，找到对象属性的watch列表，并调用watch中的update方法。

#### 4，watch通知真实的dom对象修改，或者真实dom修改通知watch，watch触发属性的修改

