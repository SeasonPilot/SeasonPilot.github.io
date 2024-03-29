Question:

Reply in Chinese (Simplified).
The following is the text content of a web page,analyze the core content and summarize:
#
07丨池化技术：如何减少频繁创建数据库连接的性能损耗,tcpdump 抓包工具在前面几节课程中,我从宏观的角度带你了解了高并发系统设计的基础知识,你已经知晓了,我们系统设计的目的是为了获得更好的性能、更高的可用性,以及更强的系统扩展能力,那么从这一讲开始,我们正式进入演进篇,我会再从局部出发,带你逐一了解完成这些目标会使用到的一些方法,比如,当然,单纯地讲解理论,讲解方案会比较枯燥,应对的过程中又涉及哪些技术点,解决思路是怎样的,接下来,公司 CEO 把你叫到会议室,时间不足的情况下,这个架构图是我们每个人最熟悉的,然后看起来就越来越复杂了,但运行平稳,但这时,因为你们数据库的调用方式是先获取数据库的连接,所以你怀疑,我用# -i: 指定网卡
tcpdump -i bond0 -nn -tttt port 4490 Copied,第三个包是客户端回给服务端的 ACK 包,第二和第三个包是客户端将加密后的密码发送给服务端的包,我们统计了一段时间的 SQL 执行时间,这在请求量小的时候其实影响不大,1s 只能执行 200 次数据库的查询,你发现解决方案也很简单,查询性能大大的提升了,其实,来说明一下连接池管理的关键点,如果连接池中有空闲连接则复用空闲连接,如果等待超过了这个设定时间则向用户抛出错误,有哪些关键点,店里一共摆着 10 台按摩椅（类比最大连接数）,有顾客来的时候,那你就会新启动一台,稍等一会儿,那顾客直接去空出来的那台按摩椅就可以了,对于数据库连接池,你需要注意池子中连接的维护问题,一般情况下,MySQL 有个参数是 wait_timeout,所以当我们使用这个被关闭的连接时就会发生错误,比如使用连接发送 select 1 的命令给数据库看是否会抛出异常,也是我比较推荐的方式,就是控制是否开启这个验证,你彻底搞清楚了连接池的工作原理,你分析了一下这个需求,进一步想,因为有了上次数据库的教训,#
用线程池预先创建线程果不其然,它的执行原理类似上面我们说的按摩椅店的模式,由当前空闲的线程执行,当线程数达到 maxTheadCount 时还有新的任务提交,首先,也就是需要执行大量 CPU 运算的任务,降低任务执行效率,但是,就可以在单位时间内执行更多的任务,当线程数超过 coreThreadCount 之后会优先创建线程,线程池中使用的队列的堆积量也是我们需要监控的重要指标,长时间都没有被执行的诡异问题,导致任务在线程池里面大量的堆积,作为一个重要的监控指标放到了系统监控大屏上,只要任务对实时性要求不高,一旦内存空间被占满就会频繁地触发 Full GC,你在系统里加上了这个特性,这时,也比较消耗系统资源,这是一种常见的软件设计思想,降低了对象的使用的成本,比方说存储池子中的对象肯定需要消耗多余的内存,这在一定程度上增加了系统启动时间,我们就可以使用池化技术来优化,后面又使用线程池提升了并行查询数据库的性能,我在面试时,后面还是需要根据实际运行情况做调整,如果池子未经过预热可能会导致系统重启后产生比较多的慢请求,你可能会用到其他的池化技术,又因池化技术踩过哪些坑,就是预先创建出所有的核心线程,// 对于 JDK 的 threadPoolExecutor 来说可以获得队列中元素个数
threadPoolExecutor.getQueue().size() Copied,每隔几分钟去检查一次,相比于业务来说很少了文中说的最小连接数是 10 和最大连接数是 20-30,这个数是如何计算出来的,有没有参考标准或者计算公式,根据具体的业务场景或者规模,有什么可以套用的配置经验吗,其实这些是经验所得,这个数值需要在实际运行中来调整,初期可以按照这个来设置,

Answer:

回复中文（简体）。
这是一篇关于池化技术的文章，主要介绍了如何使用连接池、线程池和对象池来提高高并发系统的性能、可用性和扩展性。文章的核心内容可以概括为：

- 连接池可以减少频繁创建和关闭数据库连接的开销，提高数据库查询效率，需要注意连接的维护和验证问题。
- 线程池可以减少频繁创建和销毁线程的开销，提高并行处理能力，需要注意线程数、队列长度和任务类型的选择问题。
- 对象池可以减少频繁创建和回收对象的开销，提高对象复用率，需要注意对象的初始化和清理问题。

文章还结合了作者的实际经验和案例，给出了一些配置和监控的建议。

<hr/>

