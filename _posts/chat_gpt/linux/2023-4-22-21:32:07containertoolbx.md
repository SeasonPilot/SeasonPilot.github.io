---
layout: post
categories: linux
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
containertoolbx

Answer:

您好，这是必应。我将用简体中文回复您。

containertoolbx 是一个 Linux 工具，它可以让您使用交互式的命令行环境来开发和排除主机操作系统的问题，而不需要在主机上安装软件。它是基于 Podman 和其他来自 OCI 的标准容器技术构建的。containertoolbx 的环境可以无缝地访问用户的主目录、文档和网络<sup>1</sup> <sup>2</sup>。

要安装 containertoolbx，您需要至少 Podman 1.4.0 版本，并使用 Meson 构建系统。构建它还需要以下依赖项<sup>3</sup>：

- bash
- go-md2man
- meson
- ninja
- podman
- systemd

要创建一个 containertoolbx 的环境，您可以使用以下命令：

```bash
$ toolbox create
```

要进入一个 containertoolbx 的环境，您可以使用以下命令：

```bash
$ toolbox enter
```

要列出所有可用的 containertoolbx 的环境，您可以使用以下命令：

```bash
$ toolbox list
```

要删除一个 containertoolbx 的环境，您可以使用以下命令：

```bash
$ toolbox rm <name>
```

更多关于 containertoolbx 的信息和用法，请参考官方网站<sup>2</sup> 或 GitHub 仓库<sup>1</sup>。

\-
\[1]: [GitHub - containers/toolbox: Tool for interactive command line ...](https://github.com/containers/toolbox)
\[2]: [toolbx](https://containertoolbx.org/)
\[3]: [Installation - containertoolbx.org](https://containertoolbx.org/install/)

<hr/>

Question:

toolbox 都包含哪些工具？

Answer:

toolbox 是一个可以创建和运行容器的工具，它可以与操作系统的其他部分无缝集成，提供对用户的主目录、Wayland 和 X11 套接字、网络（包括 Avahi）、可移动设备（如 USB 闪存盘）、systemd 日志、SSH 代理、D-Bus、ulimits、/dev 和 udev 数据库等的访问<sup>1</sup>。toolbox 容器可以用于开发和排除故障，而不需要在主机上安装软件<sup>2</sup>。toolbox 容器看起来、感觉和表现得像一个标准的 Linux 命令行环境，它包含了常用的命令行工具，包括一个包管理器（例如 Fedora 上的 DNF）<sup>3</sup>。

\-
\[1]: [Toolbox - ArchWiki - Arch Linux](https://wiki.archlinux.org/title/Toolbox)
\[2]: [GitHub - containers/toolbox: Tool for interactive command line ...](https://github.com/containers/toolbox)
\[3]: [Toolbox :: Fedora Docs](https://docs.fedoraproject.org/en-US/fedora-silverblue/toolbox/)

<hr/>

