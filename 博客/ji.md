import 和require一起用时报错

Cannot assign to read only property 'exports' of object '#<Object>'

解决办法

**npm install babel-plugin-transform-es2015-modules-commonjs**

　　然后在 babelrc中配置

```
　　{ "plugins": ["transform-es2015-modules-commonjs"] }
```