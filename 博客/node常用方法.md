## require.resolve

```
require.resolve("webpack-cli");
```

作用是获取这个模块所在的路径，此操作只返回文件名，不加载该模块。找不到会抛出MODULE_NOT_FOUND异常。所以可以用try catch来判断模块是否安装了。

### path.resolve

将路径或者路径片段解析成绝对路径

给定路径序列会从右向左逐渐添加，例如

```
path.resolve('/foo/bar', './baz');
// Returns: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// Returns: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// If the current working directory is /home/myself/node,
// this returns '/home/myself/node/wwwroot/static_files/gif/image.gif'
```

### require("ajv")

avj检测是否是json格式

