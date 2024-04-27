Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
'while' statement cannot complete without throwing an exception

Answer:

[1]: https://stackoverflow.com/questions/28113856/while-statement-cannot-complete-without-throwing-an-exception-android "java - 'while' statement cannot complete without throwing an exception ..."
[2]: https://wenku.csdn.net/answer/214a2cca248c4242b84e04d738560976 "'while' statement cannot complete without throwing an exception"
[3]: https://www.coder.work/article/624391 "java - 'while' 语句无法在不抛出异常的情况下完成 - Android - IT工具网"
[4]: https://stackoverflow.com/questions/47779938/whiletrue-does-not-equals-whilefalse "java - while(true) does not equals while(!false) - Stack Overflow"
[5]: https://softwareengineering.stackexchange.com/questions/297832/throwing-an-exception-when-a-method-does-not-complete-or-implement-a-work-around "Throwing an exception when a method does not complete or implement a ..."

这个错误通常发生在你的 `while` 循环中没有退出条件（或者退出条件不正确）的情况下，导致程序进入死循环，最终抛出异常以中止程序。为了解决这个问题，你需要确保 `while` 循环有正确的退出条件。例如，你可以使用 `break` 或者 `return` 语句来跳出循环，或者使用条件语句来判断是否需要进入下一次循环。同时，你也可以在循环中打印一些信息来帮助你找出问题所在<sup>1</sup>[2]。

如果你是在使用 Android Studio 或 IntelliJ，你可以在包含无限循环的方法上方添加以下代码来抑制警告：
```java
@SuppressWarnings("InfiniteLoopStatement")
```
或者在循环语句上方添加以下“魔法”注释：
```java
//noinspection InfiniteLoopStatement
```
这将告诉 IDE 这是可以接受的<sup>2</sup>[1]。

总之，确保你的 `while` 循环有明确的退出条件，以避免无限循环并抛出异常。
\-
\[1]: ['while' statement cannot complete without throwing an exception](https://wenku.csdn.net/answer/214a2cca248c4242b84e04d738560976)
\[2]: [java - 'while' statement cannot complete without throwing an exception ...](https://stackoverflow.com/questions/28113856/while-statement-cannot-complete-without-throwing-an-exception-android)
\[3]: [java - 'while' 语句无法在不抛出异常的情况下完成 - Android - IT工具网](https://www.coder.work/article/624391)
\[4]: [java - while(true) does not equals while(!false) - Stack Overflow](https://stackoverflow.com/questions/47779938/whiletrue-does-not-equals-whilefalse)
\[5]: [Throwing an exception when a method does not complete or implement a ...](https://softwareengineering.stackexchange.com/questions/297832/throwing-an-exception-when-a-method-does-not-complete-or-implement-a-work-around)

<hr/>

