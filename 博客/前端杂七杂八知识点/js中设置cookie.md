cookie中各属性对应的含义见上文

 document.cookie很奇特，打印它时会打印出出来当前域名下所有cookie列表。如下图

![image-20200811160208661](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200811160208661.png)

但是在修改cookie时却不是对这个字符串进行操作。本以为是把需要的cookie全部列出复制给document.cookie就可以，单发现这样并不能成功设置cookie。经测试发现应该一条条赋值给document.cookie，而我们多次用document.cookie="testkey:cctest"的时候只会替换当前的testkey这个cookie的值。而不修改其他的值。



#### 1，获取cookie

```
function getCookie(c_name) {
    if (document.cookie.length > 0) {
        let c_start = document.cookie.indexOf(c_name + "=");//获取字符串的起点
        if (c_start != -1) {
            c_start = c_start + c_name.length + 1;//获取值的起点
            let c_end = document.cookie.indexOf(";", c_start);//获取结尾处
            //如果是最后一个，结尾就是cookie字符串的结尾
            if (c_end == -1) c_end = document.cookie.length;
            return document.cookie.substring(c_start, c_end);//截取字符串返回
        }
    }
    return "";
}
```

### 2，设置cookie



```
function edCookie(c_name,value){
    document.cookie=`${c_name}=${value};path=/`;
    return false;
}
```

注：这里虽然用了document.cookie=，但是此操作只会覆盖cookie里c_name对应的cookie值，其余的cookie值不会进行替换。

其中pash=/是指定的cookie生效的路径可以不写。但是有些浏览器不指定会设置不成功。

这里可以设置当前c_name对应的一些列cookie属性特征，如domain、expires、等。直接在path=/后加分号加key=value即可。

![image-20200811160639349](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200811160639349.png)

### 3，删除cookie

删除cookie时，不能直接把这项值给删除了，只能通过上诉修改cookie的方式，把过期时间设置为当前。如下所示。

```
function deletCookie(c_name){
    document.cookie=`${c_name}=${getCookie(c_name)};path=/;expires=${new Date(1)};`;
    return false;

}
```

注：有时候会设置不成功，那么设置的时候加上path=/。

还有看下httponly是否是true，如果是true证明是不能修改类型。需要在后台返回这个cookie时设置为false。