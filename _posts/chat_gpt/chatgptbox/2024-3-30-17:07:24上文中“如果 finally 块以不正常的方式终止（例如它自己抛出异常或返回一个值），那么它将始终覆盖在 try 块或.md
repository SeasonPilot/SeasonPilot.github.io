Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
finally block does not complete normally

Answer:

当你在 Java 中遇到“`finally block does not complete normally`”的警告时，这通常是因为你的 `finally` 块中包含了一个 `return` 语句。让我来解释一下。

首先，`finally` 块总是会执行，无论是否抛出了异常（并且可能被捕获）或者是否正常执行。如果 `finally` 块以不正常的方式终止（例如它自己抛出异常或返回一个值），那么它将始终覆盖在 `try` 块或 `catch` 块中所做的操作。这也意味着在这种情况下，`try` 块或 `catch` 块中的操作会丢失掉。

为了解决这个问题，你可以根据具体情况删除其中一个 `return` 语句，但最好不要在 `finally` 中使用 `return`，因为它可能导致返回的值并不是你在 `try` 或 `catch` 中期望的值<sup>1</sup> <sup>3</sup> <sup>6</sup>。

总之，避免在 `finally` 块中使用 `return` 是一个良好的实践，以确保代码的预期行为和可读性。
\-
\[1]: [关于“finally block does not complete normally”警告提示 - iHADream - 博客园](https://www.cnblogs.com/thePeaceOftheLord/p/11836772.html)
\[2]: ['finally block does not complete normally' Eclipse warning](https://stackoverflow.com/questions/17481251/finally-block-does-not-complete-normally-eclipse-warning)
\[3]: [return statement - finally block does not complete normally](https://stackoverflow.com/questions/22781437/return-statement-finally-block-does-not-complete-normally)
\[4]: [Behaviour of return statement in catch and finally](https://stackoverflow.com/questions/5701793/behaviour-of-return-statement-in-catch-and-finally)
\[5]: [eclipse warning: Finally block doesn't complete normally](https://stackoverflow.com/questions/12347512/eclipse-warning-finally-block-doesnt-complete-normally)
\[6]: [Java Finally Block | Explained With Examples - JavaBeat](https://javabeat.net/java-finally-block/)
\[7]: [finally block does not complete normallyJava(536871096)](https://www.codeease.net/programming/java/finally-block-does-not-complete-normallyJava536871096)
\[8]: [finally block does not completely normally.. - Coderanch](https://coderanch.com/t/250179/certification/finally-block-completely)
\[9]: [The finally Block (The Java™ Tutorials > Essential Java ... - Oracle](https://docs.oracle.com/javase/tutorial/essential/exceptions/finally.html)

<hr/>

Question:

上文中“如果 finally 块以不正常的方式终止（例如它自己抛出异常或返回一个值），那么它将始终覆盖在 try 块或 catch 块中所做的操作。这也意味着在这种情况下，try 块或 catch 块中的操作会丢失掉。”请举例说明，并给出示例代码

Answer:

当 `finally` 块以不正常的方式终止时，它会覆盖在 `try` 块或 `catch` 块中的操作。让我通过一个示例来说明。

假设我们有一个方法，它从数据库中获取数据并返回一个结果。我们在 `try` 块中执行数据库查询，然后在 `finally` 块中关闭数据库连接。如果我们在 `finally` 块中添加了一个 `return` 语句，它会覆盖在 `try` 块中的返回值，导致方法返回的不是预期的结果。

以下是一个示例代码：

```java
public class FinallyExample {
    public static void main(String[] args) {
        System.out.println(getDataFromDatabase());
    }

    public static String getDataFromDatabase() {
        try {
            // Simulate database query
            String result = "Data from database";
            return result; // This value will be overridden if finally block completes normally
        } finally {
            // Close database connection
            System.out.println("Closing database connection");
            // Uncomment the following line to see the issue:
            // return "Overridden value from finally block";
        }
    }
}
```

在上面的示例中，如果我们取消注释 `finally` 块中的 `return` 语句，它将覆盖在 `try` 块中的返回值。如果保持注释状态，那么方法将返回 `"Data from database"`。

因此，避免在 `finally` 块中使用 `return` 是一种良好的实践，以确保代码的预期行为。

<hr/>

