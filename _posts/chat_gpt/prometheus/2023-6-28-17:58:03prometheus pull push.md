Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
prometheus pull push

Answer:

您好，这是必应。您的搜索输入是 prometheus pull push。我将用中文（简体）回复您。

Prometheus 是一个开源的监控系统，它可以收集和存储各种指标数据。Prometheus 有两种收集指标的方法：pull 和 push。

- pull 方法是 Prometheus 服务器定期访问客户端的 HTTP 端点，获取它们的指标数据。这种方法适用于长期运行的服务或应用，但不适用于短暂或批量的任务，因为它们可能在 Prometheus 访问之前就结束了，导致指标数据丢失<sup>1</sup>。
- push 方法是客户端主动将指标数据发送给 Prometheus 服务器。这种方法适用于短暂或批量的任务，例如 cron 作业或服务级别的作业<sup>4</sup>。为了实现这种方法，Prometheus 提供了一个中间服务，叫做 Pushgateway<sup>3</sup>。客户端可以将指标数据推送到 Pushgateway，然后 Prometheus 可以从 Pushgateway 拉取指标数据<sup>5</sup>。

下面是一个使用 Pushgateway 的示例代码<sup>3</sup>：

```bash
echo "some_metric 3.14" | curl --data-binary @- http://pushgateway.example.org:9091/metrics/job/some_job
```

这行代码会将一个名为 some_metric 的指标值 3.14 推送到 Pushgateway 的 /metrics/job/some_job 端点。Prometheus 可以配置为从这个端点拉取指标数据。

希望这些信息对您有帮助。如果您还有其他问题，请继续搜索或与我聊天。😊

\-
\[1]: [Push Vs. Pull In Monitoring Systems – Giedrius Statkevičius](https://giedrius.blog/2019/05/11/push-vs-pull-in-monitoring-systems/)
\[2]: [When to use the Pushgateway | Prometheus](https://prometheus.io/docs/practices/pushing/)
\[3]: [GitHub - prometheus/pushgateway: Push acceptor for ephemeral and batch ...](https://github.com/prometheus/pushgateway)
\[4]: [Pushing metrics | Prometheus](https://prometheus.io/docs/instrumenting/pushing/)
\[5]: [Pushgateway vs Pull Model: Alternatives for Prometheus Metrics - LinkedIn](https://www.linkedin.com/advice/1/what-some-alternatives-pushgateway-pushing-metrics-prometheus)

<hr/>

