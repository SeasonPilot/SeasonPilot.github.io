---
layout: post
categories: linux
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
find <directory> -type f -name "*.c" | xargs grep "<strings>"

Answer:

你好，这是必应。我可以用中文（简体）回复你。😊

你的搜索输入是一个在Linux系统中使用的命令，它的作用是在指定的目录中查找所有以.c结尾的文件，并在这些文件中搜索包含指定字符串的行。<sup>1</sup> <sup>2</sup> <sup>3</sup>

命令的格式是：

`find <directory> -type f -name "*.c" | xargs grep "<strings>"`

其中：

- `<directory>`是你要查找的文件夹，如果是当前文件夹可以省略。
- `-type f`表示只查找文件，不包括目录或其他类型。
- `-name "*.c"`表示只查找以.c结尾的文件，这样可以避免搜索二进制文件。如果不写这个参数，表示查找所有文件。
- `|`表示将前面的命令的输出作为后面命令的输入。
- `xargs`表示将输入的每一行作为一个参数传递给后面的命令。
- `grep "<strings>"`表示在每个文件中搜索包含指定字符串的行，并输出结果。

例如，如果你想在当前目录下的所有C语言文件中查找包含`printf`的行，你可以输入：

`find . -type f -name "*.c" | xargs grep "printf"`

输出结果可能类似于：

```
./main.c: printf("Hello, world!\n");
./test.c: printf("This is a test.\n");
```

希望这对你有帮助。👍

\-
\[1]: [Find Binary Files in a Directory | Baeldung on Linux](https://www.baeldung.com/linux/find-binary-files)
\[2]: [linux 多个文件中查找字符串 hadoop 3 安装 调试 - rsapaper - 博客园](https://www.cnblogs.com/rsapaper/p/8081740.html)
\[3]: [Find 使用技巧_find -atime_吖超先生的博客-CSDN博客](https://blog.csdn.net/cablsbs/article/details/8904162)

<hr/>

