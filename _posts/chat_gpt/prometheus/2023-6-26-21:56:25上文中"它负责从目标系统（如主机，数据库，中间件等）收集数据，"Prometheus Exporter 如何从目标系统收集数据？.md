Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
Prometheus Exporter 原理

Answer:

Prometheus Exporter 是 Prometheus 的指标数据收集组件<sup>1</sup> <sup>2</sup>。它负责从目标系统（如主机，数据库，中间件等）收集数据，并把收集到的数据转换为 Prometheus 支持的时序数据格式<sup>2</sup> <sup>3</sup>。Prometheus Server 周期性地从 Exporter 暴露的 HTTP 服务地址（通常是 /metrics）拉取监控样本数据<sup>3</sup> <sup>4</sup>。

Exporter 可以是一个独立运行的程序，也可以是直接内置在监控目标中<sup>3</sup>。Prometheus 官方提供了一些常用的 Exporter，如 Node Exporter（用于采集主机的运行指标），HAProxy Exporter（用于采集 HAProxy 的性能指标），MySQL Server Exporter（用于采集 MySQL 的状态指标）等<sup>4</sup> <sup>6</sup>。除此之外，还有很多第三方实现的 Exporter，如 Redis Exporter，RabbitMQ Exporter 等<sup>4</sup> <sup>5</sup>。

如果因为环境原因，网络不可达的场景，Prometheus 可以使用 Pushgateway 这个组件推送 Exporter 的指标数据到远端 Prometheus<sup>2</sup>。

以下是一个使用 Node Exporter 采集主机数据的示例<sup>3</sup>：

- 在主机上安装并启动 Node Exporter
- 在 Prometheus 配置文件中添加 Node Exporter 作为一个抓取目标
- 在 Prometheus Web UI 中查看 Node Exporter 暴露的指标数据

```yaml
# Prometheus 配置文件
global:
  scrape_interval:     15s # 抓取间隔
  evaluation_interval: 15s # 评估间隔

scrape_configs:
  - job_name: 'node' # 抓取任务名称
    static_configs:
      - targets: ['localhost:9100'] # Node Exporter 的地址
```

```bash
# 查看 Node Exporter 暴露的指标数据
curl http://localhost:9100/metrics
```

\-
\[1]: [Prometheus客户端工具process-exporter监控进程是否存在_江畔独步的博客-CSDN博客](https://blog.csdn.net/liuwei0376/article/details/114594172)
\[2]: [Node Exporter 简介_node_exporter_富士康质检员张全蛋的博客-CSDN博客](https://blog.csdn.net/qq_34556414/article/details/113107269)
\[3]: [使用Node Exporter采集主机数据 · Prometheus中文技术文档](https://www.prometheus.wang/quickstart/use-node-exporter.html)
\[4]: [Prometheus系列--Exporter原理 - 知乎](https://zhuanlan.zhihu.com/p/273229856)
\[5]: [Exporters and integrations | Prometheus](https://prometheus.io/docs/instrumenting/exporters/)
\[6]: [图解 | 监控系统 Prometheus 的原理 - 掘金](https://juejin.cn/post/7222900960791478328)

<hr/>

Question:

上文中"它负责从目标系统（如主机，数据库，中间件等）收集数据，"Prometheus Exporter 如何从目标系统收集数据？

Answer:

根据搜索结果  ，Prometheus Exporter 通过暴露一个 HTTP 服务地址（通常是 /metrics），提供标准格式的监控样本数据。Prometheus 会周期性地调用这个地址来获取数据。Exporter 可以是一个独立运行的程序，也可以是内置在监控目标中的组件。不同的 Exporter 可以采集不同的指标，比如 CPU、内存、磁盘等。

您想要了解哪种类型的 Exporter？您想要监控哪些指标？


<hr/>

