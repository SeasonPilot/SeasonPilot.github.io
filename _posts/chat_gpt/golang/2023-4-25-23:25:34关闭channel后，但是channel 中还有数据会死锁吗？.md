---
layout: post
categories: golang
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
关闭channel后，但是channel 中还有数据会死锁吗？

Answer:

你好，这是必应。我可以用中文回答你的问题。😊

根据搜索结果<sup>1</sup> <sup>2</sup> <sup>3</sup> <sup>4</sup> <sup>5</sup>，关闭channel后，但是channel中还有数据，不会死锁，但是会导致panic。因为向一个已经关闭的channel发送数据，会引起panic<sup>3</sup> <sup>5</sup>。如果继续从一个已经关闭的channel读取数据，会得到零值<sup>3</sup>。

为了避免这种情况，应该遵循以下原则<sup>1</sup> <sup>2</sup>：

- 不要在消费端关闭channel，不要在有多个并行的生产者时对channel执行关闭操作。
- 应该只在唯一的或者最后剩下的生产者协程中关闭channel，来通知消费者已经没有值可以继续读了。
- 可以使用for range循环来从channel中读取数据，当channel关闭时，循环会自动结束。
- 可以使用ok-idiom模式来判断channel是否关闭，即val, ok := <-ch，如果ok为false，代表channel已经关闭。

下面是一个示例代码<sup>2</sup>：

```go
package main

import (
	"fmt"
	"time"
)

func writeChan(c chan int) {
	for i := 0; i < 3; i++ {
		c <- i
	}
	close(c) // 关闭channel
}

func main() {
	c := make(chan int)
	go writeChan(c)
	for v := range c { // 使用for range循环读取数据
		fmt.Println(v)
	}
	time.Sleep(time.Second)
}
```

\-
\[1]: [如何优雅的关闭Go Channel【译】 - 知乎 - 知乎专栏](https://zhuanlan.zhihu.com/p/32529039)
\[2]: [由channel产生的几种死锁和panic总结 - 简书](https://www.jianshu.com/p/f25cdd72efce)
\[3]: [go 从已关闭的channel读取数据 - CSDN博客](https://blog.csdn.net/qq_41065919/article/details/107729571)
\[4]: [netty——Channl的常用方法、ChannelFuture、CloseFuture - CSDN博客](https://blog.csdn.net/qq_44027353/article/details/121332486)
\[5]: [golang 中 channel 的详细使用、使用注意事项及死锁分析 - 九卷 - 博客园](https://www.cnblogs.com/jiujuan/p/16014608.html)

<hr/>

