## 在npm里执行webpack入口源码



我们一般使用webpack时都是在package里scripts中配置启动脚本，如下

```
"scripts": {
    "start": "webpack --config ./build/webpack.config.js",
  },
```

如果webpack是局部安装的话，真正运行的语句是

```
node node_modules/.bin/webpack --config ./build/webpack.config.js
```

这是npm run时查找规则，会先查找node_modules/.bin下的文件，可以看到有webpack。

下图启动时webpack和webpack-cli的相互调用图。


![image-20200624114936492](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200624114936492.png)

接下来我们开始来看下具体逻辑代码。

#### 1，node_modules/.bin/webpack入口文件里代码

我们先把具体实现收起来，可以看到本文件，主要实现的逻辑是三个判断。主要实现的逻辑是：

a，判断是否安装了webpack-cli或者webpack-command，

b，如果安装了，调用cli的入口文件

c，没有安装提示安装，用户选择是否安装。

d，如果同时有webpack-cl和webpack-command提示卸载一个。

![image-20200624135741134](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200624135741134.png)

下边代码逻辑为加载运行cli或者command下的package.json，并运行文件中的bin里命令

```
else if (installedClis.length === 1) {
	const path = require("path");
	const pkgPath = require.resolve(`${installedClis[0].package}/package.json`);
	// eslint-disable-next-line node/no-missing-require
	const pkg = require(pkgPath);
	// eslint-disable-next-line node/no-missing-require
	require(path.resolve(
		path.dirname(pkgPath),
		pkg.bin[installedClis[0].binName]  //运行cli或者command下的package.json文件中的bin里命令
	));
}
```

### 2,打开webpack-cli下的package.json，可以看到，如下代码。

```
"bin": {
    "webpack-cli": "bin/cli.js"
  },
```

这样我们继续追踪cli.js。

cli.js里有一个重要组件是yargs，作用是读取命令行参数，具体用法可以到对应的npm下查看。

在文件里我们可以看到如下代码。可以看出cli的主要作用是读取命令行参数然后组装后传递给webpack。

![image-20200624140910621](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200624140910621.png)

这里调用的webpack是 node_modules/webpack/lib/webpack.js文件