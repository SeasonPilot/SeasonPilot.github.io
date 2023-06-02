---
layout: post
categories: golang
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
golang net/http RoundTripper

Answer:

您好，这是必应。我将用中文（简体）回复您。😊

golang net/http RoundTripper 是一个接口，它定义了如何发送 HTTP 请求并接收响应。它的唯一方法是 RoundTrip，它接受一个 *http.Request 参数，并返回一个 *http.Response 和一个 error。<sup>1</sup>

如果您想自定义您的 http.Client 的行为，例如添加超时、重试、认证、日志等功能，您可以实现自己的 RoundTripper，并将其赋值给 http.Client 的 Transport 字段。<sup>2</sup>

例如，下面的代码展示了如何实现一个简单的 RoundTripper，它在每个请求和响应上打印一些信息：

```go
type LoggingRoundTripper struct {
    rt http.RoundTripper
}

func (l *LoggingRoundTripper) RoundTrip(r *http.Request) (*http.Response, error) {
    fmt.Println("Request:", r.Method, r.URL)
    resp, err := l.rt.RoundTrip(r)
    if err != nil {
        return nil, err
    }
    fmt.Println("Response:", resp.Status)
    return resp, nil
}

func main() {
    client := &http.Client{
        Transport: &LoggingRoundTripper{http.DefaultTransport},
    }
    resp, err := client.Get("https://www.google.com")
    if err != nil {
        log.Fatal(err)
    }
    defer resp.Body.Close()
    // do something with resp.Body
}
```

如果您想了解更多关于 golang net/http RoundTripper 的内容，您可以参考以下视频<sup>3</sup>，它详细地解释了如何使用 RoundTripper 来实现不同的功能。

\-
\[1]: [http package - net/http - Go Packages](https://pkg.go.dev/net/http)
\[2]: [Diving deep into net/http : A look at http.RoundTripper](https://lanre.wtf/blog/2017/07/24/roundtripper-go)
\[3]: [Go (Golang) http RoundTripper Explained - YouTube](https://www.youtube.com/watch?v=UERCdBrka-o)

<hr/>

