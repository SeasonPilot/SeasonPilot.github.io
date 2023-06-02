---
layout: post
categories: c语言
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
fatal error: 'sys/epoll.h' file not found #include <sys/epoll.h> ^~~~~~~~~~~~~ 1 error generated.

Answer:

您好，这是必应。这个错误是因为您的系统中没有sys/epoll.h这个头文件，它是Linux内核的一部分，只能在Linux系统中使用。如果您是在MacOS或Windows上编译，您需要使用其他的库来代替epoll，比如libuv<sup>1</sup> <sup>3</sup>。您可以用homebrew安装libuv<sup>3</sup>：

```bash
brew install libuv
```

然后在您的代码中包含libuv的头文件，而不是sys/epoll.h。请问您是在什么系统和环境下编译的？您是否需要更多关于libuv的信息？

\-
\[1]: [max osx build fatal error: 'sys/epoll.h' file not found #897 - GitHub](https://github.com/uNetworking/uWebSockets/issues/897)
\[2]: [How to fix "fatal error: 'sys/epoll.h' file not found" in OSX?](https://stackoverflow.com/questions/55591983/how-to-fix-fatal-error-sys-epoll-h-file-not-found-in-osx)
\[3]: [Is cygwin possible to install epoll.h on win10? - Stack Overflow](https://stackoverflow.com/questions/67087834/is-cygwin-possible-to-install-epoll-h-on-win10)

<hr/>

