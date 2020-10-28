let stat=fs.statSync 返回stat对象

stat.isDirectory()是否是目录

fs.readFileSync(path,[encoding,flag])读取路径文件的内容，以encoding编码输出



path.extname() 返回path的扩展名就是.后边的

path.relative(frompath,topath)返回from到to的相对路径，也就是在from用to时的相对路径

```
path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');
// 返回: '../../impl/bbb'
```



crypto模块加密

```js
const crypto = require('crypto');

const secret = 'abcdefg';
const hash = crypto.createHmac('sha256', secret)
                   .update('I love cupcakes')
                   .digest('hex');
```

readline逐行读取

