---
layout: post
categories: golang
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
Go语言内存区域（mspan或mlarge）

Answer:

您好，这是Bing。我会用简体中文回复您。😊

Go语言内存区域（mspan或mlarge）是Go语言内存管理的基本组件之一。mspan是一组连续的内存页，用于存储同一大小的对象<sup>1</sup> <sup>2</sup>。mlarge是一种特殊的mspan，用于存储大于32KB的对象<sup>3</sup>。

Go语言内存管理还包括以下组件：

- mcache：每个P（处理器）都有一个mcache，用于缓存本地分配的mspan。mcache中有一个长度为numSpanClass（134）的数组，每个元素指向一个mspan<sup>1</sup> <sup>2</sup>。
- mcentral：全局的，每个mcentral用于管理相同大小的mspan。mcentral中有一个长度为numSpanClass（134）的数组，每个元素是一个mspan链表<sup>1</sup> <sup>2</sup>。
- mheap：全局的，用于管理Go语言的整个堆空间。mheap中有一个长度为numSpanClass（134）的数组，每个元素是一个mcentral<sup>1</sup> <sup>2</sup>。
- heapArena：在x86_64上用于管理64MB的堆空间。一个heapArena下有多个mspan<sup>2</sup>。

Go语言内存分配的过程大致如下：

- 如果分配的对象小于16B，则使用微小对象分配器（tiny allocator），从当前P的mcache中分配一个tiny span，并从其中切割一块内存返回<sup>2</sup> <sup>3</sup>。
- 如果分配的对象大于16B且小于32KB，则使用正常对象分配器（normal allocator），根据对象大小找到对应的span class，从当前P的mcache中分配一个对应大小的mspan，并从其中切割一块内存返回。如果mcache中没有可用的mspan，则从对应的mcentral中获取一个mspan，并放入mcache中。如果mcentral中也没有可用的mspan，则从mheap中获取一组连续的页，并创建一个新的mspan，并放入mcentral和mcache中<sup>2</sup> <sup>3</sup>。
- 如果分配的对象大于32KB，则使用大对象分配器（large allocator），直接从mheap中获取一组连续的页，并创建一个mlarge，并返回其地址<sup>2</sup> <sup>3</sup>。

Go语言内存区域（mspan或mlarge）的代码定义如下：

```go
// A span represents a run of pages.
type mspan struct {
	next *mspan // in a span linked list
	prev *mspan // in a span linked list
	startAddr uintptr // address of first byte of the span aka s.base()
	npages uintptr // number of pages in span
	allocCount uint16 // number of allocated objects in this span
	spanclass spanClass // size class and noscan (uint8)
	state uint8 // mspaninuse etc
	needzero uint8 // needs to be zeroed before allocation
	divMul uint16 // for divide by elemsize - divMagic.mul
	baseMask uintptr // if non-0, elemsize is a power of 2, & this will get object allocation base
	allocCache uint64 // cache of bits indicating which words have free objects (see alloc.go)
	allocBits *uint64 // bitmap showing which objects are free
	gcmarkBits *uint8 // bitmap showing which objects are marked (during mark phase)
	sweepgen uint32 // sweep generation, see comment in mheap.go
	divShift uint8 // for divide by elemsize - divMagic.shift
	divShift2 uint8 // for divide by elemsize - divMagic.shift2
	elemsize uintptr // computed from sizeclass or from npages
	unusedsince int64 // first time spotted by gc in mspanfree state
	npreleased uintptr // number of pages released to the os

\-
\[1]: [GO内存管理：内存组件之mspan、mcache、mcentral 和 mheap 数据结构 - G1733 - 博客园](https://www.cnblogs.com/shiqi17/p/16260438.html)
\[2]: [Golang 1.14中内存分配、清扫和内存回收 - 简书](https://www.jianshu.com/p/c40772f6b0ff)
\[3]: [Golang's memory allocation - SoByte](https://www.sobyte.net/post/2022-04/golang-memory-allocation/)
\[4]: [详解Go语言的内存模型及堆的分配管理 - 知乎 - 知乎专栏](https://zhuanlan.zhihu.com/p/76802887)

<hr/>

Question:

上文中"mcache 、mcentral、mheap、heapArena"之间什么关系？

Answer:

mcache、mcentral、mheap、heapArena之间的关系如下：

- mcache是每个P（处理器）的本地缓存，用于存储一些已切分好的mspan，以便快速分配内存给对象<sup>2</sup> <sup>4</sup> <sup>6</sup>。
- mcentral是全局的，用于管理一种特定大小的mspan，包括已分配出去的和未分配出去的。每个mcentral对应一种mspan，当mcache中没有可用的mspan时，会从mcentral中获取一个mspan，并放入mcache中<sup>2</sup> <sup>4</sup> <sup>6</sup>。
- mheap是全局的，用于管理Go语言的整个堆空间。mheap中有一个长度为numSpanClass（134）的数组，每个元素是一个mcentral。mheap还维护了一个treap结构，用于管理空闲的连续页。当mcentral中没有可用的mspan时，会从mheap中获取一组连续的页，并创建一个新的mspan，并放入mcentral和mcache中<sup>2</sup> <sup>3</sup> <sup>6</sup>。
- heapArena是在x86_64上用于管理64MB的堆空间。一个heapArena下有多个mspan。heapArena是为了解决虚拟地址空间过大而引入的概念<sup>2</sup> <sup>5</sup>。

简单来说，mcache、mcentral、mheap是三层缓存结构，用于减少内存分配的冲突和延迟。heapArena是为了保留整个虚拟地址空间而设计的。

\-
\[1]: [SegmentFault 思否](https://segmentfault.com/a/1190000039815122)
\[2]: [GO内存管理：内存组件之mspan、mcache、mcentral 和 mheap 数据结构 - G1733 - 博客园](https://www.cnblogs.com/shiqi17/p/16260438.html)
\[3]: [白话Go语言内存管理三部曲（一）内存分配原理 - 知乎](https://zhuanlan.zhihu.com/p/225190602)
\[4]: [golang 内存分配深度分析_惜暮的博客-CSDN博客](https://blog.csdn.net/u010853261/article/details/102945046)
\[5]: [7.1 设计原则 | Go 语言原本](https://golang.design/under-the-hood/zh-cn/part2runtime/ch07alloc/basic/)
\[6]: [Golang 内存之mspan、mcache、mcentral 和 mheap 数据结构 – haodro.com](http://haodro.com/archives/335126)

<hr/>

Question:

你可以通过类比的方法，解释一下吗？

Answer:

好的，我可以尝试用类比的方法来解释一下。你可以把mcache、mcentral、mheap、heapArena想象成一个快递公司的不同部门：

- mcache是每个快递员的背包，里面放着一些已经打包好的快递，以便快速送给客户。
- mcentral是每个分拣中心，负责管理一种特定大小的快递，包括已经发出去的和还没有发出去的。每个分拣中心对应一种快递，当快递员的背包里没有合适的快递时，会从分拣中心领取一个快递，并放入背包里。
- mheap是总部，负责管理整个公司的快递资源。总部有一个长度为134的数组，每个元素是一个分拣中心。总部还维护了一个树状结构，用于管理空闲的仓库。当分拣中心没有可用的快递时，会从总部申请一组连续的仓库，并创建一个新的快递，并放入分拣中心和背包里。
- heapArena是一块土地，用于建造64个仓库。一个heapArena下有多个快递。heapArena是为了解决土地资源过大而引入的概念。

简单来说，mcache、mcentral、mheap是三层缓存结构，用于减少快递分配的冲突和延迟。heapArena是为了保留整个土地资源而设计的。


<hr/>

Question:

上文"当分拣中心没有可用的快递时，会从总部申请一组连续的仓库，并创建一个新的快递，并放入分拣中心和背包里。"一组连续的仓库是指什么？

Answer:

一组连续的仓库是指在物理上相邻的仓库，比如1号仓库和2号仓库，或者3号仓库和4号仓库。这样的仓库可以被合并成一个更大的仓库，用于存放更大的快递。在Go语言中，一组连续的页（page）是指在内存地址上相邻的页，比如0x1000和0x2000，或者0x3000和0x4000。这样的页可以被合并成一个更大的mspan，用于分配更大的对象。


<hr/>

Question:

上文中"heapArena是一块土地，用于建造64个仓库。一个heapArena下有多个快递。"快递是指什么？

Answer:

快递是指mspan，也就是一组连续的页，用于分配给对象。一个heapArena下有多个mspan，也就是多个快递。heapArena是为了保留整个虚拟地址空间而引入的概念，因为在x86_64上，虚拟地址空间有48位，也就是256TB，这个空间太大了，不可能一次性申请。所以Go语言把虚拟地址空间分成了64MB的块，每个块就是一个heapArena。当需要申请内存时，就从heapArena中获取一页或者多页。


<hr/>

