---
layout: post
categories: linux
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
《On-the-fly garbage collection: an exercise in cooperation.》 — Edsger W. Dijkstra, Leslie Lamport, A. J. Martin

Answer:

您好，这是必应。我会用简体中文回复您。😊

您搜索的是一篇关于并发垃圾回收算法的论文，由 Edsger W. Dijkstra, Leslie Lamport, A. J. Martin 和 E.F.M. Steffens 四位作者于1978年发表在《ACM通讯》杂志上<sup>1</sup> <sup>2</sup> <sup>3</sup> <sup>4</sup> <sup>5</sup> <sup>6</sup>。

这篇论文提出了第一个并发垃圾回收算法，即一种允许垃圾回收器与创建垃圾的进程同时运行的算法<sup>4</sup>。这种算法利用了一种协作技术，使得两个顺序进程在频繁操作一个大型共享数据空间时，相互干扰很小<sup>5</sup>。

论文的主要思想是将数据空间划分为黑色、灰色和白色三种颜色，表示不同的状态。黑色表示已经被扫描过的对象，灰色表示正在被扫描的对象，白色表示还没有被扫描的对象。垃圾回收器的任务是将所有白色对象变成黑色对象，并回收它们所占用的空间。为了保证正确性，论文提出了一些不变式和规则，限制了两个进程对数据空间的操作<sup>5</sup>。

论文的贡献是提出了一种高效且正确的并发垃圾回收算法，为后续的研究奠定了基础。论文也展示了如何在顺序进程之间实现有效的协作，即使它们共享一个大型数据空间<sup>5</sup>。

如果您想阅读论文的全文，您可以点击以下链接<sup>4</sup> <sup>5</sup>。如果您想了解更多关于并发垃圾回收算法的信息，您可以继续搜索相关的主题。

\-
\[1]: [On-the-Fly Garbage Collection: An Exercise in Cooperation - TAU](https://www.cs.tau.ac.il/~maon/teaching/2013-2014/seminar/seminar1314b-lec11-presentation-GC.pdf)
\[2]: [On-the-fly garbage collection: an exercise in cooperation](https://www.deepdyve.com/lp/association-for-computing-machinery/on-the-fly-garbage-collection-an-exercise-in-cooperation-qNisAtJxL9)
\[3]: [A J Martin - Home](https://dl.acm.org/profile/81100391556)
\[4]: [On-the-fly Garbage Collection: an Exercise in Cooperation](https://research.microsoft.com/en-us/um/people/lamport/pubs/garbage.pdf)
\[5]: [On-the-fly garbage collection: an exercise in cooperation](https://dl.acm.org/doi/10.1145/359642.359655)
\[6]: [On-the-Fly Garbage Collection: An Exercise in Cooperation](https://www.cs.utexas.edu/users/mckinley/395Tmm/talks/Mar-30-Dijkstra.pdf)

<hr/>

