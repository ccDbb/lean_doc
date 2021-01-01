## webpack解析less、css

在项目里我们引用css文件时，需要使用css-loader加载css文件转化为common.js对象，插入到代码里去。

还需要使用style-loader将样式通过<style>标签插入到样式中。

### 解析css

##### 1,安装css-loader、syle-loader

```
npm install css-loader style-loader -D
```

##### 2,配置webpack.config.js

```
 {
   test:/\.(css)$/,
   loader:[
     'style-loader',
     'css-loader'
   ]
 }
```

loader加载顺序是从右向左，所以我们加载时是先加载了css-loader，最后调用style-loader把生成的css写入header里。

### 解析less

解析less用到的是less-loader，先将less解析成css，然后通过css-loader和style-loader插入html中。

##### 1，安装less-loader

```
npm install less-loader -D
```

##### 2，配置webpack.config.js

```
{
  test:/\.(css|less)$/,
  loader:[
    'style-loader',
    'css-loader',
    'less-loader'
    ]
}
```

### 验证

在index.vue中引入common.css或者common.less，

![image-20200621165329813](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200621165329813.png)

打包后在浏览器里预览，可以样式改变了。

代码示例https://github.com/ccDbb/webpack-test中history的v5版本中。