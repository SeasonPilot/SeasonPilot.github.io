---
layout: post
categories: golang
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
go build -ldflags="-extldflags --static"

Answer:

您好，这是必应。我可以用中文（简体）回答您的问题。😊

`go build -ldflags="-extldflags --static"`是一个用于构建Go程序的命令，它可以指定一些链接器选项。其中，`-ldflags`是一个传递给Go链接器的标志，`-extldflags`是一个传递给外部链接器（例如gcc）的标志，`--static`是一个让外部链接器生成静态链接的选项<sup>1</sup> <sup>3</sup>。

使用这个命令可以生成一个不依赖于动态库的可执行文件，这样可以在不同的系统上运行，或者在没有安装相应库的系统上运行<sup>3</sup> <sup>5</sup>。但是，这个命令也有一些限制和注意事项：

- 如果您的程序使用了cgo（即调用了C语言的代码），那么您可能需要安装musl或其他支持静态链接的C库<sup>3</sup>。
- 如果您的程序使用了多个包，并且每个包都有自己的`-extldflags`选项，那么Go链接器只会使用最后一个选项，并且忽略其他的选项<sup>2</sup>。因此，您需要把所有的`-extldflags`选项合并成一个列表传递给Go链接器。
- 如果您想要生成一个位置无关的可执行文件（PIE），那么您可能需要添加`-buildmode=pie`和`-linkmode external`等选项<sup>6</sup>。

希望这些信息对您有帮助。如果您还有其他问题，请随时提问。

\-
\[1]: [Statically compiling Go programs - arp242](https://www.arp242.net/static-go.html)
\[2]: [Statically compiled Go programs, always, even with cgo, using musl - Honnef](https://honnef.co/articles/statically-compiled-go-programs-always-even-with-cgo-using-musl/)
\[3]: [cmd/go: build: add -static flag #26492 - Github](https://github.com/golang/go/issues/26492)
\[4]: [extldflags_rpath command - github.com/bazelbuild/rules_go/tests/legacy ...](https://pkg.go.dev/github.com/bazelbuild/rules_go/tests/legacy/extldflags_rpath)
\[5]: [cmd/go: can't build a static binary since Go 1.15 #40711 - Github](https://github.com/golang/go/issues/40711)
\[6]: [Using ldflags to Set Version Information for Go Applications](https://www.digitalocean.com/community/tutorials/using-ldflags-to-set-version-information-for-go-applications)

<hr/>

Question:

上文中提到的musl是什么意思？

Answer:

上文中提到的musl是指一个C标准库的实现，它基于Linux系统调用API，包括基本语言标准、POSIX和广泛认可的扩展接口[^3^。musl是轻量、快速、简单、自由的，而且力求在标准符合性和安全性方面正确[^3^。使用musl可以生成静态链接的C程序，不依赖于其他动态库[^3^。

<hr/>

Question:

上文中提到的PIE是什么意思？

Answer:

PIE是位置无关可执行文件（Position Independent Executable）的缩写，它是一种可以在内存中任意地址加载的可执行文件，这样可以利用地址空间布局随机化（ASLR）来防止基于返回导向编程（ROP）的攻击<sup>1</sup> <sup>2</sup>。

要生成一个PIE文件，可以使用`-buildmode=pie`和`-linkmode external`等选项，这样可以复用已有的共享库（shared library）的编译方式<sup>3</sup>。但是，PIE文件也有一些性能开销，因为它需要使用全局偏移表（GOT）和过程链接表（PLT）来解析符号地址<sup>1</sup> <sup>2</sup>。

\-
\[1]: [Position Independent Executables (PIE) - Red Hat](https://www.redhat.com/en/blog/position-independent-executables-pie)
\[2]: [Position Independent Executable (PIE) Performance - Red Hat](https://www.redhat.com/en/blog/position-independent-executable-pie-performance)
\[3]: [Differentiate an ELF executable from a shared library - serializethoughts](https://serializethoughts.com/2019/06/29/elf-pic-pie)
\[4]: [What is PIE.EXE? Is it Safe or a Virus? How to remove or fix it](https://windowsbulletin.com/files/exe/sams-publishing/superbible-windows-nt-win32-api/pie-exe)
\[5]: [What is the difference between "LSB executable" (ET_EXEC) and "LSB ...](https://unix.stackexchange.com/questions/472449/what-is-the-difference-between-lsb-executable-et-exec-and-lsb-shared-object)

<hr/>

