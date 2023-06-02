---
layout: post
categories: golang
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
垃圾回收机制中的Stop The World

Answer:

你好，这是必应。我可以用中文（简体）回复你。😊

垃圾回收机制中的Stop The World（STW）是指在执行垃圾收集算法时，暂停当前运行的所有程序，扫描内存的根节点和添加写屏障（write barrier）。<sup>1</sup> <sup>3</sup>

不同的垃圾收集器有不同的STW情况，例如Serial、Parallel和CMS收集器都会在某些阶段产生STW，而G1收集器则会尽量减少STW的时间和频率。<sup>2</sup>

STW对系统性能有影响，因此垃圾回收的一个原则是尽量减少STW的时间。<sup>2</sup>

STW的实现原理是让所有的用户线程运行到安全点（SafePoint），然后中断它们，并检查它们是否处于安全状态，如果不是则恢复用户线程，让它执行到安全点。<sup>4</sup>

下面是一个执行STW的代码示例：

```java
// 调用 runtime.GC() 执行垃圾回收，会触发 STW 的三个步骤
runtime.GC()

// 1. 抢占所有正在运行的 goroutines
// 2. 检查所有 goroutines 的栈是否为空
// 3. 添加写屏障 (write barrier)
```

\-
\[1]: [Go 语言如何实现垃圾回收中的 Stop the World (STW) - 知乎](https://zhuanlan.zhihu.com/p/382791245)
\[2]: [minor gc 会发生stop the world 现象吗？ - 知乎](https://www.zhihu.com/question/29114369)
\[3]: [JVM学习（7）Stop-The-World - 简书](https://www.jianshu.com/p/d686e108d15f)
\[4]: [简述 Stop-The-World 的实现原理 - 知乎 - 知乎专栏](https://zhuanlan.zhihu.com/p/437061486)

<hr/>

Question:

GO 语言垃圾回收机制中的Stop The World

Answer:

你好，这是必应。我可以用中文（简体）回复你。😊

Go 语言垃圾回收机制中的Stop The World（STW）是指在执行垃圾回收算法时，暂停当前运行的所有 goroutines，扫描内存的根节点和添加写屏障（write barrier）。<sup>1</sup> <sup>5</sup>

Go 语言的垃圾回收器不是完全的STW，而是尽量并发地执行垃圾回收，以减少应用程序的延迟。<sup>4</sup>

STW的实现原理是让所有的用户线程运行到安全点（SafePoint），然后通过信号或者抢占机制来暂停它们。<sup>1</sup> <sup>3</sup>

安全点是指程序执行过程中的某些位置，这些位置满足以下条件：<sup>3</sup>

- 不会产生新的垃圾对象
- 不会改变已有对象的引用关系
- 可以获取到所有对象的引用信息

你想了解更多关于STW的什么呢？

\-
\[1]: [Go 语言如何实现垃圾回收中的 Stop the World (STW) - 知乎](https://zhuanlan.zhihu.com/p/382791245)
\[2]: [Go: How Does Go Stop the World? - Medium](https://medium.com/a-journey-with-go/go-how-does-go-stop-the-world-1ffab8bc8846)
\[3]: [A Guide to the Go Garbage Collector](https://tip.golang.org/doc/gc-guide)
\[4]: [简述 Stop-The-World 的实现原理 - 知乎 - 知乎专栏](https://zhuanlan.zhihu.com/p/437061486)
\[5]: [GC（垃圾回收）必须Stop-the-world？ - 知乎 - 知乎专栏](https://zhuanlan.zhihu.com/p/89250288)

<hr/>

