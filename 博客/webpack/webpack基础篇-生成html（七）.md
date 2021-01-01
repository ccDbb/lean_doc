## webpack基础篇-自动生成html（七）

我们现在的代码里，html中引入的index.js是手动写入的，主要问题有：

我们打包好的文件有时候会带有hash（接下来一章会讲到），如果直接引入，则每次修改都需要手动修改引入。

HtmlWebpackPlugin让你可以用此插件为你生成一个HTML文件，使用lodash模板提供你自己的模板，或使用你自己的loader。

### 1，安装HtmlWebpackPlugin

```
npm install  html-webpack-plugin -D
```



### 2，单页面：在webpack.config.js里设置plugins

```
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
		output:{
            path: path.resolve(__dirname,"../dist"),
            filename: '[name].js',
        },
  plugins:[
    new HtmlWebpackPlugin({
       template:  path.resolve(__dirname,'../src/index.html'),
       filename: 'index.html'
     }),
  ]
}

```

template:为html模板地址

filename：生成的html的名字为index.html，相对于output.path里设置的路径。默认路径为output.path设置的路径

### 3，运行

修改模板index.html文件，把之前引入的<script src="../dist/index.js"></script>删除。

```
npm start
```

运行后可以看到dist目录除了js外，多了一个index.html文件。

打开这个文件可以看到，除了模板index.html里本来有的内容外，多了两个js引用index.js和page2.js。

### 4，多页面打包

多页面打包和单页面打包基本一致的，区别是有几个html要在plugins里new几个HtmlWebpackPlugin对象。每个对象里设置下要引入的js

如下代码(为部分代码)，程序里有index.html和page2.html，打包后生成两个页面

```
 
 module.exports = {
     entry:{
                index: path.resolve(__dirname,'../src/index.js'),
                page2: path.resolve(__dirname,'../src/page2.js'),
            },
     plugins:[
            new HtmlWebpackPlugin({
                template:  path.resolve(__dirname,'../src/index.html'),
                filename: 'index.html',
                chunks:["index"]
            }),
            new HtmlWebpackPlugin({
                template:  path.resolve(__dirname,'../src/page2.html'),
                filename: 'page2.html',
                chunks:["page2"]
            }),
     ]
 }

```

chunks：代表要加载的js名称，名称来自entry中定义的文件名

<!--如果页面比较多，这样写会很不好看，所以可以包装一个方法，自动添加-->

下表格为htmlWebpackPlugin插件的官网给出的属性及其描述。

| Name      | Default                    | Type          | Description                                                  |
| ------   | ---------------- | ---- | ------------------------------------------------------------ |
| **`title`**              | `Webpack App`                                         | `{String}`                  | The title to use for the generated HTML document             |
| **`filename`**           | `'index.html'`                                        | `{String}`                  | The file to write the HTML to. Defaults to `index.html`. You can specify a subdirectory here too (eg: `assets/admin.html`) |
| **`template`**           | ``                                                    | `{String}`                  | `webpack` relative or absolute path to the template. By default it will use `src/index.ejs` if it exists. Please see the [docs](https://github.com/jantimon/html-webpack-plugin/blob/master/docs/template-option.md) for details |          ||
| **`templateContent`**    | false                                                 | `{string|Function|false}`   | Can be used instead of `template` to provide an inline template - please read the [Writing Your Own Templates](https://github.com/jantimon/html-webpack-plugin#writing-your-own-templates) section |
| **`templateParameters`** | `false`                                               | `{Boolean|Object|Function}` | Allows to overwrite the parameters used in the template - see [example](https://github.com/jantimon/html-webpack-plugin/tree/master/examples/template-parameters) |
| **`inject`**             | `true`                                                | `{Boolean|String}`          | `true || 'head' || 'body' || false` Inject all assets into the given `template` or `templateContent`. When passing `true` or `'body'` all javascript resources will be placed at the bottom of the body element. `'head'` will place the scripts in the head element - see the [inject:false example](https://github.com/jantimon/html-webpack-plugin/tree/master/examples/custom-insertion-position) |
| **`scriptLoading`**      | `'blocking'`                                          | `{'blocking'|'defer'}`      | Modern browsers support non blocking javascript loading (`'defer'`) to improve the page startup performance. |
| **`favicon`**            | ``                                                    | `{String}`                  | Adds the given favicon path to the output HTML               |          |
| **`meta`**               | `{}`                                                  | `{Object}`                  | Allows to inject `meta`-tags. E.g. `meta: {viewport: 'width=device-width, initial-scale=1, shrink-to-fit=no'}` |
| **`base`**               | `false`                                               | `{Object|String|false}`     | Inject a [`base`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base) tag. E.g. `base: "https://example.com/path/page.html` |
| **`minify`**             | `true` if `mode` is `'production'`, otherwise `false` | `{Boolean|Object}`          | Controls if and in what ways the output should be minified. See [minification](https://github.com/jantimon/html-webpack-plugin#minification) below for more details. |
| **`hash`**               | `false`                                               | `{Boolean}`                 | If `true` then append a unique `webpack` compilation hash to all included scripts and CSS files. This is useful for cache busting |
| **`cache`**              | `true`                                                | `{Boolean}`                 | Emit the file only if it was changed                         |
| **`showErrors`**         | `true`                                                | `{Boolean}`                 | Errors details will be written into the HTML page            |
| **`chunks`**             | `?`                                                   | `{?}`                       | Allows you to add only some chunks (e.g only the unit-test chunk) |
| **`chunksSortMode`**     | `auto`                                                | `{String|Function}`         | Allows to control how chunks should be sorted before they are included to the HTML. Allowed values are `'none' | 'auto' | 'manual' | {Function}` |
| **`excludeChunks`**      | ``                                                    | `{Array.}`                  | Allows you to skip some chunks (e.g don't add the unit-test chunk) |          |
| **`xhtml`**              | `false`                                               | `{Boolean}`                 | If `true` render the `link` tags as self-closing (XHTML compliant) |