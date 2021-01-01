## webpack核心概念entry、output、loader、plugins基础用法(二)

webpack工作内容可以用官网的一个图来表示

![image-20200608103608875](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200608103608875.png)

从图中可以看出，webpack是现在js应用程序的静态打包器，当webpack处理一个程序时，会逐步找到各个模块的依赖关系形成依赖关系图，然后把这些模块打包成一个或者多个文件。

#### 1，入口文件entry

webpack处理各个模块关系时，需要有一个入口作为开端，来形成依赖关系图，entry就是用来指定这个入口文件的。

##### a、如果只是单页面应用时，入口文件只需要指定一个入口文件。默认值为`./src`

接下来我们看一个 `entry` 配置的最简单例子：

```js
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

b、如果是多页面应用，入口文件将会有多个。

```
module.exports = {
  entry：{
    page1: './src/page1.js',
    page2: './src/page2.js'
  }
};
```

page1、page2这种key将会在output中用到，也可以不用。

#### 2，输出文件output

output将会告诉webpack打包好的文件存放在哪里，文件名是什么。

##### a、单页面示例

```javascript
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```

上边示例中path表示输出的文件的路径，默认值路径是./dist，基本上打包好的文件都将会输出到这个文件夹里。其中path.resolve是获取文件的相对路径。也可以直接写成“./dist”

filename是打包后生成的js的名称。如果这个名称想用entry里的名字或者是多页面应用的话，可以用多页面示例的方法来写

##### b、多页面示例（通过占位符来确保文件名称唯一）

```
const path = require('path');
module.exports = {
    entry:
        {
            page1: path.resolve(__dirname,'../src/index.js'),
            page2: path.resolve(__dirname,'../src/page2.js'),
        },
        output:{
            path: path.resolve(__dirname,"../dist"),
            filename: '[name].js',
        }
}
```

上边例子中output里filename的形式发生了变化，[name]通过占位符来确保文件名称唯一，

【name】取值为entry对象里key的值，运行以上示例后可以在dist目录看到文件为page1.js和page2.js.

![image-20200608141007558](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200608141007558.png)

注：output这块还有输出成组件的配置参数等，后续文章里会单独介绍。

#### 3，loaders

webpack默认只支持打包js文件。当我们程序里用到vue、less、react等非js文件时，需要用loader将对应的文件转为webpack可以处理的形式。和webpack处理js一样，形成程序依赖图，最后会把这些非js文件一起打包到最终输出的js里。

在更高层面，在 webpack 的配置中 **loader** 有两个目标：

1. `test` 属性，用于标识出应该被对应的 loader 进行转换的某个或某些文件。

2. `use` 属性，表示进行转换时，应该使用哪个 loader。

   ```
   module: {
           rules: [
               { test: /\.vue$/,
                 loader: 'vue-loader',
               }
           ]
       }
   ```

   lodaer应该放在module下，rules里可以配置多个loaders，其中test为正则表达式匹配到文件，入上诉代码里

   test: /\.vue$/表示已.vue结尾的文件，loader表示要用的转换器。

   

   注：上诉代码为编译vue用到的，但是只有loader是不能正确转义vue的，需要结合plugins的插件。所以完整代码在最后。

   #### 4，plugins

   loader 被用于转换某些类型的模块，而插件比loader范围更广一些。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量，都会参与。

   想要使用一个插件，可以通过 `require()` 它，然后把它添加到 `plugins` 数组中。多数插件可以通过选项(option)自定义。

   也可以使用 `new` 操作符来创建它的一个实例，这样可以多次使用同一个插件（比如HtmlWebpackPlugin在多页面时多次使用）。

   ```
   'use strict'
   const path = require('path');
   const VueLoaderPlugin = require('vue-loader/lib/plugin');
   const webpack = require('webpack');
   module.exports = {
       entry:{
               index: path.resolve(__dirname,'../src/index.js'),
               page2: path.resolve(__dirname,'../src/page2.js'),
           },
       output:{
               path: path.resolve(__dirname,"../dist"),
               filename: '[name].js',
           },
       module: {
           rules: [
               { test: /\.vue$/,
                 loader: 'vue-loader',
               }
           ]
       },
       plugins:[
           new VueLoaderPlugin(),
           new webpack.LoaderOptionsPlugin({
               vue: {
                   compilerOptions: {
                       preserveWhitespace: false
                   }
               }
           })]
   
   }
   ```

   

   上诉例子中，plugins包含了两个插件，VueLoaderPlugin和LoaderOptionsPlugin，这两个需要先安装在使用。

   webpack里有很多插件，可以实现各种各样的功能，这些具体的之后会说的。

   #### 5，模式（mode）

   

   

   #### 完整示例

   代码目录如下：

   ![image-20200608173616095](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200608173616095.png)

   

   在index.html里直接引入dist里的index.js文件，可以访问index.html，可以看到在vue里写的文字。

   注（如果vue里有图片或者样式不会被识别，因为没有加对应的loader）

   代码示例https://github.com/ccDbb/webpack-test中history的v1版本中。

   #### 6，contextPath
   
   ###### 基础目录，**绝对路径**，用于entry的上下文，是入口文件所处目录的绝对路径。
   
   ```
   const path = require('path');
   
   module.exports = {
     context: path.resolve(__dirname, '../src')，
     entry:{
               index: './index.js',
               //如果未设置context，需要以下面方式设置入口文件路径
               page2: path.resolve(__dirname,'../src/page2.js'),
               
           },
   };
   ```
   
   （index.js相对于当前的文件的目录为../src/index.js）
   
    上诉代码中，如果设置了context，entry的值就可以直接配置为“./index.js”。打包时会直接从context所指向的目录去查找对应的文件。
   
   默认值为当前路径

### 可能遇到的错误信息

1，ERROR in ./src/view/index.vue
Module Error (from ./node_modules/vue-loader/lib/index.js):
[vue-loader] vue-template-compiler must be installed as a peer dependency, or a compatible compiler implementation must be passed via options.
 @ ./src/index.js 2:0-36 6:21-26

![image-20200608145731957](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200608145731957.png)

vue-template-compiler没有按照或者版本和vue不匹配