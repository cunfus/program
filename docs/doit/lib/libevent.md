# libevent 事件驱动网络库

选取了 [`1.4.3-stable`][1] 版本，看一下主要文件 `ll *.c | awk '{print $NF}'`，再精简下，只分析以下文件，顺带用 `cloc` 看下行数，合计 1529 行。

```bashs
buffer.c     300  基础缓冲区操作
epoll.c      257  linux 后端的事件处理机制
evbuffer.c   259  事件驱动中的缓冲区管理
event.c      713  主逻辑
```

## 基本结构



## 主逻辑






## 参考

- [libevent源码深度剖析][ref-1]

---

[1]: https://github.com/libevent/libevent/releases/tag/release-1.4.3-stable
[ref-1]: https://github.com/balloonwj/CppGuide/tree/master/articles/libevent%E6%BA%90%E7%A0%81%E6%B7%B1%E5%BA%A6%E5%89%96%E6%9E%90