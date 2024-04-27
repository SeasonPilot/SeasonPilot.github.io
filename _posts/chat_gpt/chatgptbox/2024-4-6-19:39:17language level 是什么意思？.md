Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
Lambda expressions are not supported at language level '7'

Answer:

这个错误是因为你正在使用的Java版本不支持Lambda表达式。你需要使用Java 8或更高版本的JDK。如果你在编译时遇到了这个问题，可以尝试以下几个解决方法：

1. **升级JDK版本**：确保你使用的是Java 8或更高版本的JDK。如果你的项目配置了低于Java 8的版本，你需要升级到Java 8或更高版本。

2. **修改项目配置**：在IntelliJ IDEA中，选择“File” -> “Project Structure” -> “Project”，将“Level”修改为“8 - Lambdas, type annotations etc.”。如果问题仍然存在，还可以在“Modules”中将Java版本改为8。

3. **Gradle配置**：如果你使用Gradle构建项目，可以在app的gradle文件中添加以下代码，将语言级别设置为8.0：

    ```groovy
    android {
        compileOptions {
            targetCompatibility 1.8
            sourceCompatibility 1.8
        }
    }
    ```

希望这些方法能帮助你解决问题！🙂
\-
\[1]: [java - "Lambda expressions are not supported in -source 7, use -source ...](https://stackoverflow.com/questions/69009055/lambda-expressions-are-not-supported-in-source-7-use-source-8-to-enable-lamb)
\[2]: [解决IDEA报错：Lambda expressions not supported at language level '7'](https://www.pianshen.com/article/10281496279/)
\[3]: [出现错误lambda expressions are not supported at language level 7解决方法](https://www.pianshen.com/article/533176520/)
\[4]: [Java "lambda expressions not supported at this language level"](https://stackoverflow.com/questions/22703412/java-lambda-expressions-not-supported-at-this-language-level)
\[5]: [Lambda Expressions (The Java™ Tutorials > Learning the Java Language ...](https://docs.oracle.com/javase/tutorial/java///javaOO/lambdaexpressions.html)
\[6]: [java：解决 Lambda expressions are not supported at language level ‘7‘ 错误以及 ...](https://blog.csdn.net/qq_41538097/article/details/108058139)

<hr/>

Question:

language level 是什么意思？

Answer:

在Java中，**语言级别（language level）**定义了编辑器提供的代码辅助功能。它可以与你的项目SDK不同。例如，你可以使用JDK 9并将语言级别设置为8。这样可以使字节码与Java 8兼容，同时检查确保你不使用Java 9的构造。语言级别还会影响编译。

如果你的项目配置了低于Java 8的语言级别，那么它将不支持Java 8的新特性，如Lambda表达式。因此，当你在编译或编辑代码时，确保选择了适当的语言级别以匹配你所使用的JDK版本。🙂
\-
\[1]: [Java (programming language) - Wikipedia](https://en.wikipedia.org/wiki/Java_%28programming_language%29)
\[2]: [Project structure settings | IntelliJ IDEA Documentation - JetBrains](https://www.jetbrains.com/help/idea/project-settings-and-structure.html)
\[3]: [Programming Language Levels (Lowest to Highest) - Comp Sci Central](https://compscicentral.com/programming-language-levels/)
\[4]: [java - What is Project Language level in IntelliJ IDEA? - Stack Overflow](https://stackoverflow.com/questions/17714584/what-is-project-language-level-in-intellij-idea)

<hr/>

