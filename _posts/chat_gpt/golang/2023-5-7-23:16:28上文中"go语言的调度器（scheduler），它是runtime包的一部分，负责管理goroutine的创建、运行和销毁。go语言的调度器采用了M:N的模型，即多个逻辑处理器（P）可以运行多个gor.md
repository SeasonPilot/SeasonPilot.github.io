---
layout: post
categories: golang
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
go语言 schedule

Answer:

你好，这是Bing。我可以用中文（简体）回复你。😊

go语言是一种开源的编程语言，它能让构造简单、可靠且高效的软件变得容易<sup>1</sup>。go语言的语法接近C语言，但对于变量的声明有所不同。go语言支持垃圾回收功能。go语言的并行模型是以通信顺序进程（CSP）为基础，采取类似模型的其他语言包括Occam和Limbo，但它也具有Pi运算的特征，比如通道传输<sup>1</sup>。

schedule是一个英文单词，它在中文中可以表示“计划”、“安排”、“时间表”等意思。在go语言中，schedule可以指代以下几个方面：

- go语言的调度器（scheduler），它是runtime包的一部分，负责管理goroutine的创建、运行和销毁。go语言的调度器采用了M:N的模型，即多个逻辑处理器（P）可以运行多个goroutine（G），并由多个操作系统线程（M）来支持<sup>6</sup>。
- go语言的定时器（timer），它是time包的一部分，提供了一些函数和类型来测量和显示时间，以及执行定时任务。例如，time.After(d)函数会返回一个通道，在d时间后发送一个值；time.Tick(d)函数会返回一个通道，在每隔d时间发送一个值；time.NewTimer(d)函数会创建一个新的定时器对象，它有一个C字段，是一个通道，在d时间后发送一个值[。
- go语言的任务计划库（task scheduler），它是一些第三方包或框架提供的功能，用于在指定的时间或间隔执行一些任务或函数。例如，go-schedule是一个任务计划库，它提供了一些接口和方法来创建、启动、停止和删除任务<sup>5</sup>。

以下是一些关于go语言和schedule的代码示例：

```go
// 调度器示例：创建两个goroutine并交替打印数字
package main

import (
	"fmt"
	"runtime"
)

func main() {
	runtime.GOMAXPROCS(1) // 设置逻辑处理器为1
	go printNums(1)       // 创建第一个goroutine
	go printNums(2)       // 创建第二个goroutine
	for {                 // 主goroutine阻塞
	}
}

func printNums(g int) {
	for i := 0; i < 10; i++ {
		fmt.Printf("goroutine %d: %d\n", g, i)
	}
}
```

```go
// 定时器示例：使用time.After函数实现延时打印
package main

import (
	"fmt"
	"time"
)

func main() {
	fmt.Println("Hello")
	<-time.After(2 * time.Second) // 等待2秒后从通道接收值
	fmt.Println("World")
}
```

```go
// 任务计划库示例：使用go-schedule包创建一个每隔一秒打印时间的任务
package main

import (
	"fmt"
	"time"

	"github.com/carlescere/scheduler"
)

func main() {
	job := func() {
		fmt.Println(time.Now())
	}

	// 创建一个每隔一秒执行一次job函数的任务，并返回一个控制器
	t := scheduler.Every(1).Seconds().Run(job)

	time.Sleep(5 * time.Second) // 主程序等待5秒
	t.Quit <- true              // 停止任务
}
```

\-
\[1]: [go（计算机编程语言）_百度百科](https://baike.baidu.com/item/Go/953521)
\[2]: [Go 语言教程 | 菜鸟教程](http://runoob.com/go/go-tutorial.html)
\[3]: [Golang-Scheduler原理解析_惜暮的博客-CSDN博客](https://blog.csdn.net/u010853261/article/details/84790392)
\[4]: [Go 语言开发工具 | 菜鸟教程](https://www.runoob.com/go/go-ide.html)
\[5]: [前景 · Go语言中文文档 - topgoer.com](https://topgoer.com/)
\[6]: [真香！微软出 Go 语言教程了（中文版） - 知乎专栏](https://zhuanlan.zhihu.com/p/363261637)

<hr/>

Question:

上文中"go语言的调度器（scheduler），它是runtime包的一部分，负责管理goroutine的创建、运行和销毁。go语言的调度器采用了M:N的模型，即多个逻辑处理器（P）可以运行多个goroutine（G），并由多个操作系统线程（M）来支持"详细解释下

Answer:

好的，我来详细解释一下go语言的调度器和M:N的模型。

go语言的调度器是一种特殊的两级线程模型，它使用了三个实体：G、M和P<sup>1</sup> <sup>2</sup> <sup>3</sup>。

- G（goroutine）是go语言的协程，它是一个轻量级的执行单元，可以在一个M上运行。每个G都有自己的栈空间和寄存器状态，但是它们共享堆空间和全局变量。G的创建和销毁都由go语言的runtime包管理，不需要用户手动操作。
- M（machine）是一个内核级线程，它是操作系统调度的最小单元。每个M都有自己的线程栈和寄存器状态，但是它们共享虚拟内存空间和文件描述符。M的创建和销毁都由操作系统管理，不需要用户手动操作。
- P（processor）是一个逻辑处理器，它是go语言调度器的核心。每个P都有自己的运行队列（runqueue），用于存放等待运行的G。每个P都绑定一个M，让M执行P的运行队列中的G。P的数量由GOMAXPROCS环境变量或runtime.GOMAXPROCS函数设置，一般等于CPU核心数。

go语言的调度器采用了M:N的模型，即多个逻辑处理器（P）可以运行多个goroutine（G），并由多个操作系统线程（M）来支持<sup>1</sup> <sup>2</sup> <sup>3</sup>。这样可以实现以下几个优点：

- 利用多核CPU，提高并发性能。每个P可以在不同的M上运行，从而实现真正的并行执行。
- 减少上下文切换开销，提高执行效率。每个G都很小，只占用几KB的内存空间，而且可以在同一个M上快速切换，避免了频繁地切换到内核态。
- 隐藏系统调用阻塞，提高吞吐量。当一个G因为系统调用而阻塞时，调度器会把它从当前的P上摘下来，并把另一个就绪的G放到P上运行。同时，调度器会创建或复用一个空闲的M，并把阻塞的G绑定到这个M上，等待系统调用返回。

go语言的调度器还有很多细节和优化策略，如果你想了解更多，请参考以下链接：

<sup>1</sup>: https://zhuanlan.zhihu.com/p/77620605
<sup>2</sup>: https://www.cnblogs.com/CJ-cooper/p/15270475.html
<sup>3</sup>: https://www.jianshu.com/p/4afa0679851d

\-
\[1]: [[译] Go语言调度器 - 知乎 - 知乎专栏](https://zhuanlan.zhihu.com/p/77620605)
\[2]: [【golang详解】go语言GMP(GPM)原理和调度 - CJ-cooper - 博客园](https://www.cnblogs.com/CJ-cooper/p/15270475.html)
\[3]: [【深度知识】GO语言的goroutine并发原理和调度机制 - 简书](https://www.jianshu.com/p/4afa0679851d)

<hr/>

