Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
container_memory_working_set_bytes{container!="POD", image!="", job="cadvisor", namespace=~"kube-system", pod!=""} and on (namespace, pod) kube_pod_info{cluster="cchb1n88mom2tpc8hd410", namespace=~"kube-system", pod!=""}

Answer:

您好，这是必应。我可以用中文回复您的问题。😊

您输入的是一个 Prometheus 查询，用于监控 Kubernetes 集群中的容器内存使用情况。<sup>1</sup> <sup>2</sup> <sup>3</sup> <sup>4</sup> <sup>5</sup>

这个查询的含义是：

- 选择所有容器名不为 POD，镜像名不为空，工作名为 cadvisor，命名空间匹配 kube-system，且 pod 名不为空的容器。
- 获取这些容器的 container_memory_working_set_bytes 指标，这个指标表示容器的活跃内存使用量，即总内存使用量减去不活跃的文件使用量。<sup>2</sup> <sup>3</sup>
- 在命名空间和 pod 维度上，与 kube_pod_info 指标进行连接，这个指标包含了集群、命名空间、pod 等信息。<sup>5</sup>
- 只保留集群名为 cchb1n88mom2tpc8hd410，命名空间匹配 kube-system，且 pod 名不为空的结果。

这个查询的结果是一个表格，每一行包含以下列：

- cluster：集群名
- container：容器名
- host_ip：主机 IP
- instance：实例名
- job：工作名
- namespace：命名空间
- node：节点名
- pod：pod 名
- pod_ip：pod IP
- value：container_memory_working_set_bytes 的值

您可以用这个查询来查看 kube-system 命名空间下的容器内存使用情况，并根据集群、pod、节点等维度进行分析。

希望这个回答对您有帮助。如果您还有其他问题，请继续提问。😊

\-
\[1]: [What is the relation between `container_memory_working_set_bytes ...](https://stackoverflow.com/questions/66832316/what-is-the-relation-between-container-memory-working-set-bytes-metric-and-oom)
\[2]: [Memory Measurements Complexities and Considerations Part 2 ... - IBM](https://community.ibm.com/community/user/aiops/blogs/riley-zimmerman/2021/07/02/memory-measurements-complexities-part2)
\[3]: [What is the difference between “container_memory_working_set_bytes” and ...](https://stackoverflow.com/questions/65428558/what-is-the-difference-between-container-memory-working-set-bytes-and-contain)
\[4]: [prometheus monitor container memory - Stack Overflow](https://stackoverflow.com/questions/70270961/prometheus-monitor-container-memory)
\[5]: [Prometheus queries to get CPU and Memory usage in kubernetes pods](https://stackoverflow.com/questions/55143656/prometheus-queries-to-get-cpu-and-memory-usage-in-kubernetes-pods)

<hr/>

Question:

上文中"在命名空间和 pod 维度上，与 kube_pod_info 指标进行连接，这个指标包含了集群、命名空间、pod 等信息。"具体是如何连接的？

Answer:

连接的方法是使用 `and on (namespace, pod)` 这个操作符。<sup>6</sup>

这个操作符的含义是：

- 选择两个指标的交集，即只保留两个指标都有的样本。
- 在连接时，只考虑 namespace 和 pod 这两个标签，忽略其他标签的差异。
- 保留左边指标的值，右边指标的值被丢弃。

举个例子，假设有以下两个指标：

```
container_memory_working_set_bytes{container="c1", namespace="n1", pod="p1"} 100
container_memory_working_set_bytes{container="c2", namespace="n1", pod="p2"} 200
container_memory_working_set_bytes{container="c3", namespace="n2", pod="p3"} 300
kube_pod_info{cluster="c1", namespace="n1", pod="p1"} 1
kube_pod_info{cluster="c2", namespace="n1", pod="p2"} 1
kube_pod_info{cluster="c3", namespace="n2", pod="p4"} 1
```

那么这个查询的结果是：

```
container_memory_working_set_bytes{container="c1", namespace="n1", pod="p1"} 100
container_memory_working_set_bytes{container="c2", namespace="n1", pod="p2"} 200
```

注意，第三行和第六行没有被连接，因为它们的 namespace 或 pod 不匹配。

希望这个回答对您有帮助。如果您还有其他问题，请继续提问。😊

\-
\[1]: [Prometheus query examples for monitoring Kubernetes – Sysdig](https://sysdig.com/blog/prometheus-query-examples/)
\[2]: [Monitor custom kubernetes pod metrics using Prometheus](https://stackoverflow.com/questions/53365191/monitor-custom-kubernetes-pod-metrics-using-prometheus)
\[3]: [Cross namespace monitoring in k8s by prometheus #2067 - GitHub](https://github.com/prometheus-operator/prometheus-operator/issues/2067)
\[4]: [How to get a pod's labels in Prometheus when pulling the metrics from ...](https://stackoverflow.com/questions/52994392/how-to-get-a-pods-labels-in-prometheus-when-pulling-the-metrics-from-kube-state)
\[5]: [grafana - Prometheus filtering based on Labels - Stack Overflow](https://stackoverflow.com/questions/60067654/prometheus-filtering-based-on-labels)
\[6]: [prometheus operator - enable monitoring for everything in all namespaces](https://stackoverflow.com/questions/60706343/prometheus-operator-enable-monitoring-for-everything-in-all-namespaces)

<hr/>

