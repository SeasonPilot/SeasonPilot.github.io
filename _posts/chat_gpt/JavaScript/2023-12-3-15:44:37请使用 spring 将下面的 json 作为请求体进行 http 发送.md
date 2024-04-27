Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
请使用 spring 将下面的 json 作为请求体进行 http 发送

Answer:

您好，这是 Bing。如果您想使用 spring 将 json 作为请求体进行 http 发送，您可以参考以下几种方法：

- 使用 HttpURLConnection 类，设置请求方法为 POST，设置请求头的 content-type 为 application/json，并使用 OutputStreamWriter 将 json 字符串写入输出流<sup>1</sup>。例如：

```java
URL url = new URL("http://example.com");
HttpURLConnection con = (HttpURLConnection) url.openConnection();
con.setRequestMethod("POST");
con.setRequestProperty("Content-Type", "application/json; utf-8");
con.setRequestProperty("Accept", "application/json");
con.setDoOutput(true);

String jsonInputString = "{\"name\": \"Upendra\", \"job\": \"Programmer\"}";

try(OutputStream os = con.getOutputStream()) {
    byte[] input = jsonInputString.getBytes("utf-8");
    os.write(input, 0, input.length);           
}
```

- 使用 Spring MVC 的 @RequestBody 注解，将请求体中的 json 数据自动反序列化为一个模型对象<sup>2</sup>。例如：

```java
@RestController

<hr/>

