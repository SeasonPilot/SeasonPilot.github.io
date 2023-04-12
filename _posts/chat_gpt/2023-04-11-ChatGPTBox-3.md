---
layout: post
categories: ChatGPTBox
---
问题:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
epoll 全局事件集合

回答:

你好，这是Bing。我可以帮你找到一些关于epoll 全局事件集合的内容和解决方案。👋

epoll 是 Linux 内核的可扩展 I/O 事件通知机制，它可以高效地监听多个文件描述符上的事件。epoll 的事件注册函数是 epoll_ctl，它可以在内核事件表中添加、修改或删除要监听的事件类型。

epoll_event 结构体是 epoll 的核心数据结构，它分为 events 和 data 两个部分。events 是 epoll 注册的事件，比如 EPOLLIN、EPOLLOUT 等等。data 是用户自定义的数据，可以是文件描述符、指针或其他整数。

epoll 的全局事件集合是一个红黑树，它存储了所有被监听的文件描述符及其对应的 epoll_event 结构体。当一个文件描述符上发生了注册的事件时，内核会将该文件描述符及其对应的 epoll_event 结构体从红黑树中移动到一个双向链表中，这个双向链表就是就绪事件集合。

epoll 有两种工作模式：LT（水平触发）和 ET（边缘触发）。LT 模式下，当一个文件描述符上有可读或可写数据时，epoll_wait 会一直返回该文件描述符，直到数据被完全处理。ET 模式下，当一个文件描述符上有可读或可写数据时，epoll_wait 只会返回一次该文件描述符，如果没有完全处理数据，下次调用 epoll_wait 时不会再返回该文件描述符，除非有新的数据到来。

以下是一个使用 epoll 的简单示例代码：

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/epoll.h>
#include <unistd.h>

#define MAX_EVENTS 10

int main()
{
    int epfd; // epoll 文件描述符
    int nfds; // 就绪事件数目
    int i; // 循环变量
    struct epoll_event ev; // 用于注册事件
    struct epoll_event events[MAX_EVENTS]; // 用于存储就绪事件
    char buf[1024]; // 缓冲区

    // 创建一个 epoll 实例
    epfd = epoll_create(1);
    if (epfd == -1) {
        perror("epoll_create");
        exit(EXIT_FAILURE);
    }

    // 设置标准输入为非阻塞模式
    fcntl(STDIN_FILENO, F_SETFL, O_NONBLOCK);

    // 注册标准输入的可读事件
    ev.events = EPOLLIN;
    ev.data.fd = STDIN_FILENO;
    if (epoll_ctl(epfd, EPOLL_CTL_ADD, STDIN_FILENO, &ev) == -1) {
        perror("epoll_ctl");
        exit(EXIT_FAILURE);
    }

    // 循环等待事件发生
    while (1) {
        // 等待就绪事件
        nfds = epoll_wait(epfd, events, MAX_EVENTS, -1);
        if (nfds == -1) {
            perror("epoll_wait");
            exit(EXIT_FAILURE);
        }

        // 处理就绪事件
        for (i = 0; i < nfds; i++) {
            if (events[i].data.fd == STDIN_FILENO) { // 如果是标准输入
                // 读取数据并输出
                int len = read(STDIN_FILENO, buf, sizeof(buf));
                if (len > 0) {
                    buf[len] = '\0';
                    printf("You input: %s\n", buf);
                }
            }
        }
    }

    // 关闭 epoll 文件描述符
    close(epfd);

    return 0;
}
```


<hr/>

问题:

详细介绍下epoll 的全局事件集合

回答:

好的，我可以详细介绍一下 epoll 的全局事件集合。👍

epoll 的全局事件集合是一个红黑树，它存储了所有被监听的文件描述符及其对应的 epoll_event 结构体。当一个文件描述符上发生了注册的事件时，内核会将该文件描述符及其对应的 epoll_event 结构体从红黑树中移动到一个双向链表中，这个双向链表就是就绪事件集合。

红黑树是一种自平衡的二叉搜索树，它可以保证在插入、删除和查找操作时，时间复杂度都是 O(log n)。红黑树的每个节点有一个颜色属性，要么是红色，要么是黑色。红黑树必须满足以下五个性质[^7^：

1. 每个节点要么是红色，要么是黑色。
2. 根节点是黑色。
3. 每个叶子节点（NIL节点，空节点）是黑色的。
4. 如果一个节点是红色的，则它的两个子节点都是黑色的。
5. 从任意节点到其每个叶子的所有路径都包含相同数目的黑色节点。

epoll 的全局事件集合使用红黑树来存储文件描述符及其对应的 epoll_event 结构体，这样可以提高查找效率，并且可以保证在添加或删除文件描述符时，不会造成树的不平衡。epoll 的全局事件集合在内核中的定义如下[^8^：

```c
struct epitem {
    struct rb_node rbn; // 红黑树节点
    struct list_head rdllink; // 双向链表节点
    struct epitem *next; // 用于 EPOLLEXCLUSIVE 模式
    struct epoll_filefd ffd; // 文件描述符
    struct epoll_event event; // 事件类型和用户数据
    struct rcu_head rcu; // 用于延迟释放
};

struct eventpoll {
    struct mutex mtx; // 互斥锁
    struct rw_semaphore pollsem; // 读写锁
    wait_queue_head_t wq; // 等待队列
    wait_queue_head_t poll_wait; // 轮询等待队列
    struct list_head rdllist; // 就绪事件集合
    struct rb_root_cached rbr; // 全局事件集合
    struct epitem *ovflist; // 溢出列表
};
```


<hr/>

