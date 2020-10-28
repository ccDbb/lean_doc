## wabpack基础篇-watch监听（六）

在前边几篇文章中，我们可以正常打包js、css、vue等文件，但是每次修改文件时都需要手动重新编译，生成index.js文件。

webpack中提供watch可以解决这个问题。watch有两种使用方法：

一种是在运行webpack时直接在在后边添加--watch

另一种在webpack.config.js中配置。

### 方法一：在webpack.config.js中添加watch属性，和watchOptions

```
 watch:true,
 watchOptions: {
     aggregateTimeout: 300,//毫秒
     poll: 1000,//秒，表示每秒检查一次变动
     ignored:/node_modules/
 }
```

- ###### watch默认是false，设置为true意味着构建之后，wabpack将监听已解析文件的更改

- watchOptions.aggregateTimeout当第一个文件更改后，会有一段时间时间的延迟，在进行重新构建。这个选项允许这段时间内任何更改都一起重新构建。这样可以达到修改代码一定时间内一起打包。默认值为300ms

- watchOptions.poll 多少毫秒内的轮询一次，查看是否有变动。通过传递 `true` 开启 ，或者指定毫秒为单位进行轮询。

- watchOption.ignored忽略监控的问价。

*webpack-dev-server 和 webpack-dev-middleware 里 Watch 模式默认开启。*

### 方法二：在package.json中webpack后添加--watch

```
 "scripts": {
    "start": "webpack --watch --config ./build/webpack.config.js",
  },
```



### 3，启动

启动后可以看到控制台打印的日志多了一条

![image-20200628104354894](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200628104354894.png)

表示监控开始。

##### watch的原理是：watch开启后，webpack会隔一段时间（poll）轮训一次要打包的文件，监听到变化，会缓存一下第一次，在一段时间时候后（aggregateTimeout设置的），检测所有修改的文件。这时候把所有修改文件一起编译打包。

代码示例https://github.com/ccDbb/webpack-test中history的v6版本中。

