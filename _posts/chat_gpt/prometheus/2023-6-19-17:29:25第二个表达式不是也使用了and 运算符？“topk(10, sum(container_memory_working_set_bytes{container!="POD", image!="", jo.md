Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
“sum(container_memory_working_set_bytes{container!="POD", image!="", job="cadvisor", namespace=~"kube-system", pod!=""} and on (namespace, pod) kube_pod_info{cluster="cchb1n88mom2tpc8hd410", namespace=~"kube-system", pod!=""}) by (pod, namespace) and topk(10, sum(container_memory_working_set_bytes{container!="POD", image!="", job="cadvisor", namespace=~"kube-system", pod!=""} and on (namespace, pod) kube_pod_info{cluster="cchb1n88mom2tpc8hd410", namespace=~"kube-system", pod!=""}) by (pod, namespace))” 和 “topk(10, sum(container_memory_working_set_bytes{container!="POD", image!="", job="cadvisor", namespace=~"kube-system", pod!=""} and on (namespace, pod) kube_pod_info{cluster="cchb1n88mom2tpc8hd410", namespace=~"kube-system", pod!=""}) by (pod, namespace))” 有什么区别？

Answer:

您好，这是必应。我可以用中文回答您的问题。😊

您输入的是 **Prometheus 查询语言**（PromQL）的表达式<sup>1</sup>。PromQL 是一种用于对存储在 Prometheus 数据库中的度量数据进行聚合、分析和算术运算的领域特定语言（DSL）<sup>2</sup>。它由各种函数和运算符组成<sup>3</sup>。

您输入的两个表达式的区别是：

- 第一个表达式使用了 `and` 运算符，它会返回两个操作数都为真的样本<sup>4</sup>。这意味着，只有当 `container_memory_working_set_bytes` 和 `kube_pod_info` 都有相同的 `pod` 和 `namespace` 标签时，才会返回结果。
- 第二个表达式没有使用 `and` 运算符，它会返回所有满足条件的样本，不管它们是否有相同的标签。
- 因此，第一个表达式的结果可能比第二个表达式的结果更少，也可能更准确，因为它会排除那些没有匹配标签的样本。

您想要查询什么类型的数据？您可以使用 PromQL 的函数和运算符来修改您的表达式，以获得更精确或更广泛的结果<sup>5</sup>。

\-
\[1]: [Querying basics | Prometheus](https://prometheus.io/docs/prometheus/latest/querying/basics/)
\[2]: [Prometheus Query Language - Prometheus Definitive Guide Part II](https://www.infracloud.io/blogs/promql-prometheus-guide/)
\[3]: [Prometheus Query Language - LinkedIn](https://www.linkedin.com/pulse/prometheus-query-language-marcel-koert)
\[4]: [Querying examples | Prometheus](https://prometheus.io/docs/prometheus/latest/querying/examples/)
\[5]: [Query functions | Prometheus](https://prometheus.io/docs/prometheus/latest/querying/functions/)

<hr/>

Question:

直接使用第二个表达式不就可以了？ 为什么还要用第一个呢？ 返回的结果应该是一样的

Answer:

不一定。第二个表达式可能会返回一些没有匹配标签的样本，这些样本可能不是您想要的。例如，如果有一个 pod 有 `container_memory_working_set_bytes` 的数据，但没有 `kube_pod_info` 的数据，那么它会被包含在第二个表达式的结果中，但不会被包含在第一个表达式的结果中。这可能会导致您得到错误的数据或排序。


<hr/>

Question:

为什么会被包含在第二个表达式的结果中？

Answer:

因为第二个表达式没有使用 `and` 运算符，它会返回所有满足条件的样本，不管它们是否有相同的标签。如果您想要只返回有匹配标签的样本，您可以使用 `and` 运算符，或者使用 `group_left` 或 `group_right` 函数[^5^。


<hr/>

Question:

第二个表达式不是也使用了and 运算符？“topk(10, sum(container_memory_working_set_bytes{container!="POD", image!="", job="cadvisor", namespace="kube-system", pod!=""} and on (namespace, pod) kube_pod_info{cluster="cchb1n88mom2tpc8hd410", namespace="kube-system", pod!=""}) by (pod, namespace))” 

Answer:

不是的。第二个表达式只在 `sum` 函数中使用了 `and` 运算符，它会对两个操作数进行求和，然后返回结果。但是，这个结果并没有被用于 `topk` 函数，而是被忽略了。如果您想要使用 `and` 运算符来过滤结果，您需要把它放在 `topk` 函数的外面，或者使用 `group_left` 或 `group_right` 函数。


<hr/>

