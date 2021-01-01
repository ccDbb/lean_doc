## webpack解析es6（三）

上一节中，我们看webpack核心组成部门时，以解析.vue文件为例进行的。

webpack原生支持js语法，但是es6有很多新特性，有些浏览器和webpack并不能很好的理解，这时需要借助babel来进行把es6的语法转为es5语法。

### 一、webpack解析es6

使用的解析组件是babel-loader，而babel呢是需要依赖babel，所以我们用的时候需要安装babel。



新版本的babel进行了更加详细的拆分，按需安装即可。

##### 1，我们这里先本地安装babel-cli

```
npm install --save-dev @babel/core @babel/preset-env babel-loader
```

新版的babel，安装形式为@babel/core，之前的版本是babel-core，形式不同只是代表不同的版本号。

我们是用来解析es6的所有只用到core和preset-env就可以了，所以这里边我们只安装这个。

##### 2，新建babel的配置.babelrc文件，和packjson同级

.babelrc的内容（推荐内容）想要深入了解babel的可以访问它的官网https://www.babeljs.cn/docs/usage

```
{

  "presets": [
    "@babel/preset-env"
  ]


  "plugins": [],
}
```

在.babelrc文件中一般会有presets和plugins两个属性值，presets更像是功能的集合，plugins对应的是每一个功能点，之后文章会细讲这部分，或者可以直接去babel官网查看。

##### 3，在webpack.config.js中module的rules下新增一个loader

```
 module: {
        rules: [
            { test: /\.vue$/,
              loader: 'vue-loader',
            },
            { test: /\.js$/,
                loader: 'babel-loader',
            },
        ]
    },
```
test: /\.js$/表示匹配到所有已js结尾的文件，都用babel这个loader。

修改后运行npm start打包，可以看到打包后的文件已经改变。

babel还有好多相关组件，以后用到什么可以在单独安装什么，比如transform-es2015-modules-commonjs，AMD和common的转化等



##### 总结

在没有使用babel时，我们看下打包后的截图，可以看到代码里用到的es6的语法打包后依然是es6的语法

![image-20200618230116417](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200618230116417.png)

### 

而在使用babel后可以看到的文件中es6的语法被转化成了es5的语法（下图红框里内如）

![image-20200618230247400](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200618230247400.png)





##### 代码示例https://github.com/ccDbb/webpack-test中history的v3版本中。