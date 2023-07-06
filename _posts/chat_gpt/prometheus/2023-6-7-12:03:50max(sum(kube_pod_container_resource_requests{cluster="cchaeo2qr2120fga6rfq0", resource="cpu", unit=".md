Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
max(sum(kube_pod_container_resource_requests{cluster="cchaeo2qr2120fga6rfq0", resource="cpu", unit="core"}) by (cluster, node) / on (cluster, node) kube_node_status_allocatable{cluster="cchaeo2qr2120fga6rfq0", resource="cpu", unit="core"})

Answer:

你好，这是必应。你的搜索输入是一个用于计算 Kubernetes 集群中每个节点的 CPU 利用率的 Prometheus 查询<sup>1</sup> <sup>2</sup>。这个查询的含义是：

- `kube_pod_container_resource_requests{cluster="cchaeo2qr2120fga6rfq0", resource="cpu", unit="core"}`：这个指标表示每个 Pod 容器请求的 CPU 资源量，单位是核心<sup>3</sup>。这里只选择了集群为 `cchaeo2qr2120fga6rfq0` 的指标。
- `sum(...) by (cluster, node)`：这个函数表示按照集群和节点对 Pod 容器的 CPU 资源请求量进行求和，得到每个节点上所有 Pod 容器请求的 CPU 资源总量。
- `kube_node_status_allocatable{cluster="cchaeo2qr2120fga6rfq0", resource="cpu", unit="core"}`：这个指标表示每个节点可分配给 Pod 的 CPU 资源量，单位也是核心<sup>2</sup>。这里也只选择了集群为 `cchaeo2qr2120fga6rfq0` 的指标。
- `/ on (cluster, node)`：这个操作表示按照集群和节点对两个指标进行除法，得到每个节点上所有 Pod 容器请求的 CPU 资源占可分配 CPU 资源的比例，即 CPU 利用率。
- `max(...)`：这个函数表示从所有节点中选择最大的 CPU 利用率。

因此，这个查询的结果是集群 `cchaeo2qr2120fga6rfq0` 中 CPU 利用率最高的节点的 CPU 利用率值。如果这个值超过 100%，则表示有些 Pod 容器使用了超过其请求量的 CPU 资源<sup>4</sup>。

你可以使用 Grafana 来可视化这个查询的结果，或者使用其他工具来监控和优化你的 Kubernetes 集群的资源管理。

你还有其他关于 Kubernetes 或 Prometheus 的问题吗？

\-
\[1]: [Understanding Kubernetes Limits and Requests – Sysdig](https://sysdig.com/blog/kubernetes-limits-requests/)
\[2]: [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)
\[3]: [kube-state-metrics/pod-metrics.md at main - GitHub](https://github.com/kubernetes/kube-state-metrics/blob/main/docs/pod-metrics.md)
\[4]: [Grafana for Kubernettes shows CPU usage higher than 100%](https://stackoverflow.com/questions/61361263/grafana-for-kubernettes-shows-cpu-usage-higher-than-100)

<hr/>

