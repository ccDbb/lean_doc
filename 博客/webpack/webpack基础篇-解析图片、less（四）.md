## webpack解析图片

如果我们直接引入的图片是网上链接对应的图片，那么是可以不用图片解析器的。

如果是在图片放在本项目的路径内引入就需要用的图片解析器。常用的图片解析器有file-loader和url-loader

当我们引入本地图片，而没有用对应loader时会看到如下报错

![image-20200620100735931](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200620100735931.png)

url-loader是把图片转为base64字节的文件，在options里可以设置最大图片大小。如果超过这个值，就会和file-loader行为一样，打包后会生成单独的图片文件放在dist目录。

这篇我们就以url-loader为例

### 安装url-loader

```
npm install url-loader --save-dev
```

本地安装file-loader

### 在webpackconfig中配置url-loader

在module的rules中添加如下代码

```
{ test: /\.(png|jpe?g|gif|svg)$/,
  loader: 'url-loader',
},
```

（完整代码可以到github上查看，文章底部有地址链接）

### 运行打包命令

```
npm start
```

打开引入打包后js的html文件，可以看到图片是以base64模式显示的。

![image-20200620130952149](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200620130952149.png)

### 在代码中引用

如图引入图片相对位置即可

![image-20200620131409692](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200620131409692.png)



如果我们用file-loader来进行打包，

#### 安装file-loader

```
npm install file-loader --save-dev
```

#### 在webpackconfig中配置file-loader

```
{ test: /\.(png|jpe?g|gif|svg)$/,
  loader: 'file-loader',
  options: {
  	publicPath:"../dist"
  }
},
```

其中publicPath为打包后在html中插入图片的位置相对路径。

### 打包

```
npm start
```

打包后可以看到dist目录里多了一个图片

![image-20200620131617739](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200620131617739.png)

### 代码里引用

因为我们没有用生成html的loader，所以如果我们直接像url-loader里那般引用的话，在浏览器里打开html这个图片src会是一个object对象。

我们可以换一种方式来引入

![image-20200620132122483](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200620132122483.png)

运行html可以看到图片是以地址的形式引入的。

![image-20200620132158315](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200620132158315.png)

这是两种图片的loader，一般直接用url-loader就可以满足了。

##### 代码示例https://github.com/ccDbb/webpack-test中history的v4版本中。