chrome进程架构

现在chrome浏览器由一个浏览器主进程、一个GPU进程、一个网络进程，多个渲染进程和多个插件进程

每个非同源的页签各有一个渲染进程。

主进程：负责页面交互

渲染进程：负责加载html、css、js渲染页面，默认情况下每个tab标签就有一个渲染进程，如果是同源就共用同一个进程

GPU进程：实现3D css效果

网络进程：负责加载网络资源。之前属于主进程里的

插件进程：负责插件的运行。

