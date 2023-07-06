Question:

Reply in Chinese (Simplified).
以下是一篇文章,标题是:"
            一文了解Golang的map增量扩容
             ",作者是:"
    谈笑风生间
  ",内容是:
".markdown-body .octicon{display:inline-block,fill:currentColor,vertical-align:text-bottom}.markdown-body .anchor{float:left,line-height:1,margin-left:-20px,padding-right:4px}.markdown-body .anchor:focus{outline:none}.markdown-body h1 .octicon-link,.markdown-body h2 .octicon-link,.markdown-body h3 .octicon-link,.markdown-body h4 .octicon-link,.markdown-body h5 .octicon-link,.markdown-body h6 .octicon-link{color:#1b1f23,vertical-align:middle,visibility:hidden}.markdown-body h1:hover .anchor,.markdown-body h2:hover .anchor,.markdown-body h3:hover .anchor,.markdown-body h4:hover .anchor,.markdown-body h5:hover .anchor,.markdown-body h6:hover .anchor{text-decoration:none}.markdown-body h1:hover .anchor .octicon-link,.markdown-body h2:hover .anchor .octicon-link,.markdown-body h4:hover .anchor .octicon-link:before,background-image:url("data:image/svg+xml,Segoe UI,font-size:16px,monospace,font-size:inherit,.markdown-body hr:before{display:table,.markdown-body h4,margin-bottom:10px}.markdown-body blockquote{margin:0}.markdown-body ol,.markdown-body ul ol ol,font-size:12px}.markdown-body pre{margin-top:0,border-color:#0366d6}.markdown-body .border{border:1px solid #e1e4e8,important}.markdown-body .text-gray-light{color:#6a737d,important}.markdown-body .pl-c{color:#6a737d}.markdown-body .pl-c1,.markdown-body .pl-sr,color:#22863a}.markdown-body .pl-ml{color:#735c0f}.markdown-body .pl-mh,background-color:#ffeef0}.markdown-body .pl-mi1{color:#22863a,important,important}.markdown-body .pl-1{padding-left:4px,important}.markdown-body .pl-5{padding-left:32px,important}.markdown-body .pl-11{padding-left:112px,Menlo,border:1px solid #d1d5da,important}.markdown-body a:not([href]){color:inherit,.markdown-body table,border:0}.markdown-body blockquote{padding:0 1em,.markdown-body h6{margin-top:24px,color:#6a737d}.markdown-body ol,font-size:1em,.markdown-body table th{padding:6px 13px,background-color:rgba(27,font-size:100%,overflow:auto,padding:0,border:0}.markdown-body .commit-tease-sha{display:inline-block,color:#444d56}.markdown-body .full-commit .btn-outline:not(:disabled):hover{color:#005cc5,padding-left:10px,line-height:20px,white-space:nowrap,31,vertical-align:top}.markdown-body .blob-code-inner{overflow:visible,color:#24292e,tab-size:2}.markdown-body .tab-size[data-tab-size="3"]{-moz-tab-size:3,tab-size:9}.markdown-body .tab-size[data-tab-size="10"]{-moz-tab-size:10,background:#f8f8f8}.hljs-comment,.hljs-number,font-weight:700}.hljs-subst{font-weight:400}.hljs-class .hljs-title,.hljs-regexp{color:#009926}.hljs-bullet,hash表大小始终为2的整数倍,这个过程不是一次性完成的,并不会把旧的bucket从oldbucket中删除,如耗时更长等
只有当oldbucket中所有bucket移动到新表后,也会触发扩容,too small and we waste a lot of space. I wrote
// a simple program to check some stats for different loads:
// (64-bit,// so keep the same number of buckets and "grow" laterally.
    // B+1 相当于之前的2倍空间
	bigger := uint8(1)
    // 对应条件2
	if,nil)

    // 对标志位的处理
    // &^表示 按位置0
    // x=01010011
    // y=01010100
    // z=x&^y=00000011
    // 如果y的bit位为1,= nil {
		// Promote current overflow buckets to the old generation.
		if h.extra.oldoverflow,h,那么 bucketmask 的低 5 位是 11111,oldbucket*uintptr(t.bucketsize)))
	// 结果是2^B,用x来搬迁
		var xy [2]evacDst
		x := &xy[0]
		x.b = (*bmap)(add(h.buckets,dataOffset)
			y.e = add(y.k,dataOffset)
			e := add(k,uintptr(t.keysize)),h.sameSizeGrow() {
					// Compute hash to make our evacuation decision (whether we need
					// to send this key/elem to bucket x or bucket y).
                    // 计算hash值,t.reflexivekey() &&,as our evacuation decision must
						// match whatever decision the iterator made.
						// Fortunately,表示搬到useT部分（可能是x也可能是y,k) // copy elem
				}
                // 如果v是指针,uintptr(t.elemsize))
			}
		}
        // 如果没有协程在用老的bucket,n)
		}
	}
    
    // 如果此次搬迁的bucket等于当前搬迁进度,确保行为是O(1)的
	// Experiments suggest that 1024 is overkill by at least an order of magnitude.
	// Put it in there as a safeguard anyway,= nil {
			h.extra.oldoverflow = nil
		}
        // 清除正在扩容的标志位
		h.flags &^= sameSizeGrow
	}
}
复制代码
源码里提到 X,一个 bucket 中的 key 会分裂落到 2 个桶中,并向前“多看”一位,取决于 hash 值 第 6 bit 位是 0 还是 1,表示key的搬迁去向
参考

go语言设计与实现
golang修养之路
go语言笔试面试宝典
".各个评论如下:
.请以如下格式输出你的回答：
          {文章摘要和文章作者}
          ======
          {文章总结和对文章的看法}
          ======
          {对评论的总结},分配到 X part,如果是 1,则分配到 Y part
已搬迁完的key的tophash值是一个状态值,表示key的搬迁去向
参考

go语言设计与实现
golang修养之路
go语言笔试面试宝典
".各个评论如下:
.请以如下格式输出你的回答：
          {文章摘要和文章作者}
          ======
          {文章总结和对文章的看法}
          ======
          {对评论的总结},

Answer:

这篇文章的标题是"一文了解Golang的map增量扩容"，作者是"谈笑风生间"，内容是介绍了Golang中map的扩容机制和源码分析，包括了bucket的结构、hash值的计算、key的分配和搬迁、扩容的触发条件和过程等。文章使用了代码片段和注释来解释了map的内部实现，也提供了一些参考资料。
======
文章总结和看法：

文章是一篇比较深入的技术文章，针对Golang中map这个常用的数据结构，揭示了它的底层原理和设计思想。文章对map的扩容机制进行了详细的分析，展示了map是如何在保证性能和空间利用率的同时，实现动态增长和并发安全的。文章对于想要深入了解Golang语言特性和优化技巧的读者有一定的参考价值，但也需要一定的基础知识和阅读能力，才能理解文章中的代码和概念。
======
对评论的总结：

根据文章下方的评论，可以看出大部分读者对文章表示了赞赏和感谢，认为文章内容丰富、深入浅出、有助于学习。也有一些读者提出了自己的疑问或建议，比如关于map的性能测试、扩容策略、内存管理等方面。还有一些读者分享了自己的学习心得或相关资源，比如关于Golang的书籍、博客、视频等。总体来说，评论反映了读者对文章的高度关注和积极互动。


<hr/>

Question:

什么是等量扩容

Answer:

等量扩容是Golang中map的一种扩容机制，当map的元素数量达到一定比例时，会触发扩容，将bucket的数量增加一倍，同时将旧的bucket中的key分配到新的bucket中，这个过程是渐进式的，不会一次性完成。等量扩容可以减少hash冲突，提高map的性能和空间利用率。<sup>1</sup> <sup>3</sup> <sup>4</sup>

<sup>1</sup>: [Golang Map实现（四） map 的赋值和扩容 - 搬砖程序员带你飞 - 博客园](https://www.cnblogs.com/-lee/p/12807063.html)
<sup>3</sup>: [php - 深入理解 Go map：赋值和扩容迁移 - 煎鱼的清汤锅 - SegmentFault 思否](https://segmentfault.com/a/1190000018632347)
<sup>4</sup>: [Go maps in action - The Go Programming Language](https://go.dev/blog/maps)
\-
\[1]: [Golang Map实现（四） map 的赋值和扩容 - 搬砖程序员带你飞 - 博客园](https://www.cnblogs.com/-lee/p/12807063.html)
\[2]: [php - 深入理解 Go map：赋值和扩容迁移 - 煎鱼的清汤锅 - SegmentFault 思否](https://segmentfault.com/a/1190000018632347)
\[3]: [Go maps in action - The Go Programming Language](https://go.dev/blog/maps)
\[4]: [Golang Map解析：用法，源码分析 - 知乎 - 知乎专栏](https://zhuanlan.zhihu.com/p/161511413)
\[5]: [golang 如何定义一个map类型的const变量啊？ - 知乎](https://www.zhihu.com/question/25953192)

<hr/>

Question:

“如果负载因子没有超标，但是使用的溢出桶较多，也会触发扩容。但是是等量扩容

原因是原桶中有太多的键值对被删除，等量扩容可以使得剩余的键值对排列更加紧凑，节省空间”是什么意思？

Answer:

这句话的意思是，Golang中map有一个负载因子，用来衡量map的填充程度，当map的元素数量超过负载因子乘以bucket的数量时，就会触发扩容。bucket是map的基本存储单元，每个bucket最多可以存储8个键值对。如果一个bucket已经满了，还有新的键值对要放进去，就会创建一个溢出桶，挂在原来的bucket后面。溢出桶会增加map的空间占用和查找时间。所以，即使map的元素数量没有超过负载因子，但是溢出桶太多，也会触发扩容，这样可以重新分配键值对到新的bucket中，减少溢出桶的数量，提高map的效率。<sup>1</sup> <sup>2</sup> <sup>3</sup>

<sup>1</sup>: [深度解析golang map - 掘金](https://juejin.cn/post/6954707500151078919)
<sup>2</sup>: [Go map底层结构 - 掘金](https://juejin.cn/post/6988820056570495013)
<sup>3</sup>: [聊聊golang map的实现细节 - 掘金](https://juejin.cn/post/6977302491520040996)

\-
\[1]: [深度解析golang map - 掘金](https://juejin.cn/post/6954707500151078919)
\[2]: [Go map底层结构 - 掘金](https://juejin.cn/post/6988820056570495013)
\[3]: [聊聊golang map的实现细节 - 掘金](https://juejin.cn/post/6977302491520040996)

<hr/>

Question:

bucket的数量对应hmap 中哪个字段？

Answer:

bucket的数量对应hmap中的B字段，B是一个uint8类型的变量，表示bucket的数量为2^B个。<sup>1</sup> <sup>2</sup> <sup>3</sup>

<sup>1</sup>: [GOLANG MAP's underlying implementation - Programmer All](https://www.programmerall.com/article/71751050134/)
<sup>2</sup>: [map | 袁昊的学习笔记 - GitHub Pages](https://howieyuen.github.io/docs/golang/data-structure/map/)
<sup>3</sup>: [go/src/runtime/map.go at master · golang/go · GitHub](https://github.com/golang/go/blob/master/src/runtime/map.go)

\-
\[1]: [GOLANG MAP's underlying implementation - Programmer All](https://www.programmerall.com/article/71751050134/)
\[2]: [map | 袁昊的学习笔记 - GitHub Pages](https://howieyuen.github.io/docs/golang/data-structure/map/)
\[3]: [go/src/runtime/map.go at master · golang/go · GitHub](https://github.com/golang/go/blob/master/src/runtime/map.go)
\[4]: [dictionary - Why does the bucket of map in golang contain up to 8 key ...](https://stackoverflow.com/questions/67445332/why-does-the-bucket-of-map-in-golang-contain-up-to-8-key-elem-pairs-why-the-num)
\[5]: [How the Go runtime implements maps efficiently (without generics) - Cheney](https://dave.cheney.net/2018/05/29/how-the-go-runtime-implements-maps-efficiently-without-generics)

<hr/>

Question:

"buckets是一个指向bucket数组的指针，每个bucket的索引由key的哈希值的低位决定。"是什么意思？

Answer:

这个意思是，当你使用map的时候，你需要提供一个key和一个value，比如map[key] = value。为了快速地找到key对应的value，map会先对key进行哈希运算，得到一个哈希值。哈希值是一个数字，它可以用二进制表示，比如01100101。然后，map会用哈希值的低位（也就是右边的几位）来决定key-value应该存储在哪个bucket中。bucket是一个存储单元，它可以存储最多8个key-value对。map有很多bucket，它们组成了一个数组。buckets字段就是指向这个数组的指针。<sup>1</sup> <sup>2</sup> <sup>3</sup>

<sup>1</sup>: [golang hashmap的使用及实现 - 简书](https://www.jianshu.com/p/32b839e99289)
<sup>2</sup>: [dictionary - Golang map internal implementation - how does it search the map for a key? - Stack Overflow](https://stackoverflow.com/questions/37995648/golang-map-internal-implementation-how-does-it-search-the-map-for-a-key)
<sup>3</sup>: [go/src/runtime/map.go at master · golang/go · GitHub](https://github.com/golang/go/blob/master/src/runtime/map.go)

\-
\[1]: [golang hashmap的使用及实现 - 简书](https://www.jianshu.com/p/32b839e99289)
\[2]: [Golang Maps - GeeksforGeeks](https://www.geeksforgeeks.org/golang-maps/)
\[3]: [How does go calculate a hash value for keys in a map?](https://stackoverflow.com/questions/37625480/how-does-go-calculate-a-hash-value-for-keys-in-a-map)
\[4]: [dictionary - Golang map internal implementation - how does it search ...](https://stackoverflow.com/questions/37995648/golang-map-internal-implementation-how-does-it-search-the-map-for-a-key)
\[5]: [go/src/runtime/map.go at master · golang/go · GitHub](https://github.com/golang/go/blob/master/src/runtime/map.go)

<hr/>

