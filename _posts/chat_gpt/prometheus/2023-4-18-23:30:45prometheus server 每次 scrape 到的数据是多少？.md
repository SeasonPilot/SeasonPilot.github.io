---
layout: post
categories: prometheus
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
prometheus server 每次 scrape 到的数据是多少？

Answer:

您好，这是必应。我会尽力回答您的问题。😊

Prometheus server 每次 scrape 到的数据量取决于您的配置和目标服务的指标数量。Prometheus server 通过 scrape_interval 参数设置每个 job 的抓取间隔，例如 6s，并通过 scrape_timeout 参数设置每个抓取请求的超时时间，例如 3s。如果您没有为每个 job 设置这些参数，那么它们会使用 global 配置中的默认值。

Prometheus server 通过 job 和 instance 的概念来定义抓取目标。一个 job 是一组具有相同目的的 instance，通常对应于一个单独的进程或服务。一个 instance 是一个可以抓取的端点，通常对应于一个单独的进程或服务实例。您可以通过 static_configs 或 service discovery 的方式来指定 job 和 instance 的列表。

Prometheus server 每次抓取一个 instance 时，会获取该 instance 暴露的所有指标数据，并为每个指标数据添加一个时间戳（如果没有提供的话）和一些标签（例如 job 和 instance）。指标数据的格式是 `<metric name>{<label name>=<label value>, ...} <value> [<timestamp>]`。例如：

```
go_gc_duration_seconds{quantile="1"} 4.9351e-05
go_gc_duration_seconds{quantile="0.99"} 0.00010917
go_gc_duration_seconds{quantile="0.9"} 7.1527e-05
go_gc_duration_seconds{quantile="0.5"} 4.374e-05
```

因此，Prometheus server 每次 scrape 到的数据量与您配置的 job 和 instance 的数量，以及每个 instance 暴露的指标数据的数量和大小有关。您可以通过 Prometheus web UI 的 `/targets` 页面查看每个 job 和 instance 的最近一次抓取状态和耗时。


<hr/>

Question:

每个 instance 暴露的指标数据的数量和大小有关，请举例说明

Answer:

好的，我来举例说明。假设您有两个 job，一个是 node，用于监控主机的性能指标，一个是 mysql，用于监控数据库的性能指标。每个 job 有两个 instance，分别是：

- node: 1.2.3.4:9100, 5.6.7.8:9100
- mysql: 9.10.11.12:3306, 13.14.15.16:3306

每个 instance 都会暴露一个 HTTP 服务，用于提供指标数据。例如，node exporter 会提供如下的指标数据：

```
# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 3.2095e-05
go_gc_duration_seconds{quantile="0.25"} 3.8317e-05
go_gc_duration_seconds{quantile="0.5"} 5.0845e-05
go_gc_duration_seconds{quantile="0.75"} 5.652e-05
go_gc_duration_seconds{quantile="1"} 0.000238472
go_gc_duration_seconds_sum 0.786788964
go_gc_duration_seconds_count 15916
# HELP go_goroutines Number of goroutines that currently exist.
# TYPE go_goroutines gauge
go_goroutines 8
# HELP go_info Information about the Go environment.
# TYPE go_info gauge
go_info{version="go1.15.6"} 1
# HELP go_memstats_alloc_bytes Number of bytes allocated and still in use.
# TYPE go_memstats_alloc_bytes gauge
go_memstats_alloc_bytes 4.922008e+06
...
```

每行指标数据都包含一个指标名称，一个或多个标签，一个数值和一个可选的时间戳。每个指标数据的大小取决于它的名称、标签和数值的长度。例如，`go_memstats_alloc_bytes` 的大小是 32 字节，而 `go_gc_duration_seconds{quantile="0"}` 的大小是 38 字节。

每个 instance 暴露的指标数据的数量取决于它所采集的监控对象的种类和数量。例如，node exporter 可以采集主机的 CPU、内存、磁盘、网络等多种指标，而 mysql exporter 可以采集数据库的连接数、查询数、事务数等多种指标。不同的监控对象可能有不同的指标数量和频率。例如，CPU 的使用率可能每秒变化很多次，而磁盘的使用量可能每分钟变化一次。

因此，每个 instance 暴露的指标数据的数量和大小与它所采集的监控对象的种类和数量有关。如果您想知道某个 instance 暴露了多少个指标数据，您可以使用以下查询：

```
scrape_samples_scraped{job="<job-name>", instance="<instance-id>"}
```

这个查询会返回目标暴露的样本数。如果您想知道某个 instance 暴露了多大的指标数据，您可以使用以下查询：

```
scrape_series_added{job="<job-name>", instance="<instance-id>"}
```

这个查询会返回目标暴露的样本大小（字节）。希望这些例子能帮助您理解每个 instance 暴露的指标数据的数量和大小与什么有关。


<hr/>

