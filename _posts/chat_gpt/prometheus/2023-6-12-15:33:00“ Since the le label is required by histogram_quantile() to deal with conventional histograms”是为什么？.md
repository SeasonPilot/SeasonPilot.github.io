Question:

Reply in Chinese (Simplified).Summarize the following as concisely as possible:
"histogram_count() and histogram_sum() 
Both functions only act on native histograms, which are an experimental feature. The behavior of these functions may change in future versions of Prometheus, including their removal from PromQL.

histogram_count(v instant-vector) returns the count of observations stored in a native histogram. Samples that are not native histograms are ignored and do not show up in the returned vector.

Similarly, histogram_sum(v instant-vector) returns the sum of observations stored in a native histogram.

Use histogram_count in the following way to calculate a rate of observations (in this case corresponding to “requests per second”) from a native histogram:

histogram_count(rate(http_request_duration_seconds[10m]))
The additional use of histogram_sum enables the calculation of the average of observed values (in this case corresponding to “average request duration”):

  histogram_sum(rate(http_request_duration_seconds[10m]))
/
  histogram_count(rate(http_request_duration_seconds[10m]))
histogram_fraction()
This function only acts on native histograms, which are an experimental feature. The behavior of this function may change in future versions of Prometheus, including its removal from PromQL.

For a native histogram, histogram_fraction(lower scalar, upper scalar, v instant-vector) returns the estimated fraction of observations between the provided lower and upper values. Samples that are not native histograms are ignored and do not show up in the returned vector.

For example, the following expression calculates the fraction of HTTP requests over the last hour that took 200ms or less:

histogram_fraction(0, 0.2, rate(http_request_duration_seconds[1h]))
The error of the estimation depends on the resolution of the underlying native histogram and how closely the provided boundaries are aligned with the bucket boundaries in the histogram.

+Inf and -Inf are valid boundary values. For example, if the histogram in the expression above included negative observations (which shouldn't be the case for request durations), the appropriate lower boundary to include all observations less than or equal 0.2 would be -Inf rather than 0.

Whether the provided boundaries are inclusive or exclusive is only relevant if the provided boundaries are precisely aligned with bucket boundaries in the underlying native histogram. In this case, the behavior depends on the schema definition of the histogram. The currently supported schemas all feature inclusive upper boundaries and exclusive lower boundaries for positive values (and vice versa for negative values). Without a precise alignment of boundaries, the function uses linear interpolation to estimate the fraction. With the resulting uncertainty, it becomes irrelevant if the boundaries are inclusive or exclusive.

histogram_quantile()
histogram_quantile(φ scalar, b instant-vector) calculates the φ-quantile (0 ≤ φ ≤ 1) from a conventional histogram or from a native histogram. (See histograms and summaries for a detailed explanation of φ-quantiles and the usage of the (conventional) histogram metric type in general.)

Note that native histograms are an experimental feature. The behavior of this function when dealing with native histograms may change in future versions of Prometheus.

The conventional float samples in b are considered the counts of observations in each bucket of one or more conventional histograms. Each float sample must have a label le where the label value denotes the inclusive upper bound of the bucket. (Float samples without such a label are silently ignored.) The other labels and the metric name are used to identify the buckets belonging to each conventional histogram. The histogram metric type automatically provides time series with the _bucket suffix and the appropriate labels.

The native histogram samples in b are treated each individually as a separate histogram to calculate the quantile from.

As long as no naming collisions arise, b may contain a mix of conventional and native histograms.

Use the rate() function to specify the time window for the quantile calculation.

Example: A histogram metric is called http_request_duration_seconds (and therefore the metric name for the buckets of a conventional histogram is http_request_duration_seconds_bucket). To calculate the 90th percentile of request durations over the last 10m, use the following expression in case http_request_duration_seconds is a conventional histogram:

histogram_quantile(0.9, rate(http_request_duration_seconds_bucket[10m]))
For a native histogram, use the following expression instead:

histogram_quantile(0.9, rate(http_request_duration_seconds[10m]))
The quantile is calculated for each label combination in http_request_duration_seconds. To aggregate, use the sum() aggregator around the rate() function. Since the le label is required by histogram_quantile() to deal with conventional histograms, it has to be included in the by clause. The following expression aggregates the 90th percentile by job for conventional histograms:

histogram_quantile(0.9, sum by (job, le) (rate(http_request_duration_seconds_bucket[10m])))
When aggregating native histograms, the expression simplifies to:

histogram_quantile(0.9, sum by (job) (rate(http_request_duration_seconds[10m])))
To aggregate all conventional histograms, specify only the le label:

histogram_quantile(0.9, sum by (le) (rate(http_request_duration_seconds_bucket[10m])))
With native histograms, aggregating everything works as usual without any by clause:

histogram_quantile(0.9, sum(rate(http_request_duration_seconds[10m])))
The histogram_quantile() function interpolates quantile values by assuming a linear distribution within a bucket.

If b has 0 observations, NaN is returned. For φ < 0, -Inf is returned. For φ > 1, +Inf is returned. For φ = NaN, NaN is returned.

The following is only relevant for conventional histograms: If b contains fewer than two buckets, NaN is returned. The highest bucket must have an upper bound of +Inf. (Otherwise, NaN is returned.) If a quantile is located in the highest bucket, the upper bound of the second highest bucket is returned. A lower limit of the lowest bucket is assumed to be 0 if the upper bound of that bucket is greater than 0. In that case, the usual linear interpolation is applied within that bucket. Otherwise, the upper bound of the lowest bucket is returned for quantiles located in the lowest bucket."

Answer:

好的，我会用中文回复你。以下是我对你给的文本的简要概括：

这段文本介绍了四个PromQL函数，分别是histogram_count()，histogram_sum()，histogram_fraction()和histogram_quantile()，它们都可以用来处理直方图数据。直方图数据有两种类型，一种是传统的直方图，另一种是实验性的原生直方图。这些函数的用法和效果可能会因为原生直方图的特性而发生变化。

histogram_count(v instant-vector)和histogram_sum(v instant-vector)分别返回原生直方图中观测值的数量和总和。这两个函数可以结合使用来计算观测值的平均值。

histogram_fraction(lower scalar, upper scalar, v instant-vector)返回原生直方图中观测值在给定范围内的比例。这个函数使用线性插值来估计比例，误差取决于原生直方图的分辨率和给定范围与桶边界的对齐程度。

histogram_quantile(φ scalar, b instant-vector)计算传统直方图或原生直方图中的φ-分位数（0 ≤ φ ≤ 1）。这个函数需要传统直方图的每个桶有一个le标签，表示桶的上界。这个函数也使用线性插值来估计分位数。

\-
\[1]: [Chinese Text Summarization | ChineseNLP](https://chinesenlp.xyz/docs/text_summarization.html)
\[2]: [LowinLi/Text-Summarizer-Pytorch-Chinese - GitHub](https://github.com/LowinLi/Text-Summarizer-Pytorch-Chinese)
\[3]: [Text summarize](https://www.text-summarize.com/)
\[4]: [Summarization Tool for All Languages - Paraphrase Tool](https://paraphrasetool.com/blog/summarization-tool-for-all-languages)

<hr/>

Question:

conventional histogram 和 native histograms 是什么意思？ 两个的异同是什么？

Answer:

传统直方图和原生直方图都是一种用来展示数据分布的图表，它们由一系列的桶组成，每个桶表示一个数值范围，桶的高度表示该范围内的数据频数。传统直方图和原生直方图的区别在于：

- 传统直方图是一种常见的直方图类型，它的桶的边界是固定的，通常是等宽或者按照某种规则划分的。传统直方图需要在收集数据之前就确定桶的数量和边界，这可能会导致数据的精度损失或者不合适的分布展示。
- 原生直方图是一种实验性的直方图类型，它的桶的边界是动态的，根据数据的变化而变化。原生直方图可以在收集数据之后再确定桶的数量和边界，这可以提高数据的精度和分布展示的适应性。<sup>1</sup> <sup>2</sup>


\-
\[1]: [histograms: Render a conventional histogram backed by a native ... - GitHub](https://github.com/prometheus/client_golang/issues/1129)
\[2]: [Feature flags | Prometheus](https://prometheus.io/docs/prometheus/latest/feature_flags/)
\[3]: [A Complete Guide to Histograms | Tutorial by Chartio](https://chartio.com/learn/charts/histogram-complete-guide/)
\[4]: [How to Describe the Shape of Histograms (With Examples)](https://www.statology.org/describe-shape-of-histogram/)
\[5]: [Histogram - Wikipedia](https://en.wikipedia.org/wiki/Histogram)

<hr/>

Question:

“ Since the le label is required by histogram_quantile() to deal with conventional histograms”是为什么？

Answer:

这是因为histogram_quantile()函数是用来计算传统直方图的分位数的，它需要知道每个桶的上界，而le标签就是用来表示桶的上界的（le表示小于等于）。<sup>1</sup> <sup>4</sup> histogram_quantile()函数会根据le标签对桶进行排序，然后根据给定的分位数（0 ≤ φ ≤ 1）和桶的频数来计算分位数对应的数值。<sup>2</sup> <sup>3</sup> <sup>5</sup>

\-
\[1]: [histogram_quantile() - Hands-On Infrastructure Monitoring with ...](https://www.oreilly.com/library/view/hands-on-infrastructure-monitoring/9781789612349/01c927e7-224d-465f-ad14-6c1409f42c85.xhtml)
\[2]: [Query functions | Prometheus](https://prometheus.io/docs/prometheus/latest/querying/functions/)
\[3]: [How does a Prometheus Histogram work? - Robust Perception](https://www.robustperception.io/how-does-a-prometheus-histogram-work/)
\[4]: [Histograms and summaries | Prometheus](https://prometheus.io/docs/practices/histograms/)
\[5]: [Understanding histogram_quantile based on rate in Prometheus](https://stackoverflow.com/questions/55162093/understanding-histogram-quantile-based-on-rate-in-prometheus)

<hr/>

