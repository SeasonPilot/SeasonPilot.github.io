Question:

Reply in Chinese (Simplified).
The following is the text content of a web page,analyze the core content and summarize:
FUNCTIONS
abs()
absent()
absent_over_time()
ceil()
changes()
clamp()
clamp_max()
clamp_min()
day_of_month()
day_of_week()
day_of_year()
days_in_month()
delta()
deriv()
exp()
floor()
histogram_count() and histogram_sum()
histogram_fraction()
histogram_quantile()
holt_winters()
hour()
idelta()
increase()
irate()
label_join()
label_replace()
ln()
log2()
log10()
minute()
month()
predict_linear()
rate()
resets()
round()
scalar()
sgn()
sort()
sort_desc()
sqrt()
time()
timestamp()
vector()
year()
<aggregation>_over_time()
Trigonometric FunctionsSome functions have default arguments,e.g. year(v=vector(time()) instant-vector). This means that there is one argument v which is an instant vector,which if not provided it will default to the value of the expression vector(time()).Notes about the experimental native histograms:Ingesting native histograms has to be enabled via a feature flag. As long as no native histograms have been ingested into the TSDB,it will automatically convert them appropriately. (With the currently supported bucket schemas,instance=~".*"})
# => {job="myjob"}absent(sum(nonexistent{job="myjob"}))
# => {}
In the first two examples,instance=~".*"}[1h])
# => {job="myjob"}absent_over_time(sum(nonexistent{job="myjob"})[1h:])
# => {}
In the first two examples,min scalar,max scalar) clamps the sample values of all elements in v to have an upper limit of max.clamp_min()clamp_min(v instant-vector,where 0 means Sunday etc.day_of_year()day_of_year(v=vector(time()) instant-vector) returns the day of the year for each of the given times in UTC. Returned values are from 1 to 365 for non-leap years,so that it is possible to get a non-integer result even if the sample values are all integers.The following example expression returns the difference in CPU temperature between now and 2 hours ago:delta(cpu_temp_celsius{host="zeus"}[2h])
delta acts on native histograms by calculating a new histogram where each compononent (sum and count of observations,each element in v that contains a mix of float and native histogram samples within the range,using simple linear regression. The range vector must have at least two samples in order to perform the calculation. When +Inf or -Inf are found in the range vector,including their removal from PromQL.histogram_count(v instant-vector) returns the count of observations stored in a native histogram. Samples that are not native histograms are ignored and do not show up in the returned vector.Similarly,which are an experimental feature. The behavior of this function may change in future versions of Prometheus,histogram_fraction(lower scalar,the following expression calculates the fraction of HTTP requests over the last hour that took 200ms or less:histogram_fraction(0,rate(http_request_duration_seconds[1h]))
The error of the estimation depends on the resolution of the underlying native histogram and how closely the provided boundaries are aligned with the bucket boundaries in the histogram.+Inf and -Inf are valid boundary values. For example,the appropriate lower boundary to include all observations less than or equal 0.2 would be -Inf rather than 0.Whether the provided boundaries are inclusive or exclusive is only relevant if the provided boundaries are precisely aligned with bucket boundaries in the underlying native histogram. In this case,it becomes irrelevant if the boundaries are inclusive or exclusive.histogram_quantile()histogram_quantile(φ scalar,b may contain a mix of conventional and native histograms.Use the rate() function to specify the time window for the quantile calculation.Example: A histogram metric is called http_request_duration_seconds (and therefore the metric name for the buckets of a conventional histogram is http_request_duration_seconds_bucket). To calculate the 90th percentile of request durations over the last 10m,rate(http_request_duration_seconds_bucket[10m]))
For a native histogram,use the sum() aggregator around the rate() function. Since the le label is required by histogram_quantile() to deal with conventional histograms,sum by (job,the expression simplifies to:histogram_quantile(0.9,sum by (le) (rate(http_request_duration_seconds_bucket[10m])))
With native histograms,sum(rate(http_request_duration_seconds[10m])))
The histogram_quantile() function interpolates quantile values by assuming a linear distribution within a bucket.If b has 0 observations,-Inf is returned. For φ > 1,NaN is returned. The highest bucket must have an upper bound of +Inf. (Otherwise,the upper bound of the second highest bucket is returned. A lower limit of the lowest bucket is assumed to be 0 if the upper bound of that bucket is greater than 0. In that case,sf scalar,the more importance is given to old data. The higher the trend factor tf,returning an instant vector with the given deltas and equivalent labels.idelta should only be used with gauges.increase()increase(v range-vector) calculates the increase in the time series in the range vector. Breaks in monotonicity (such as counter resets due to target restarts) are automatically adjusted for. The increase is extrapolated to cover the full time range as specified in the range vector selector,buckets) is the increase between the respective component in the first and last native histogram in v. However,will be missing from the result vector.increase should only be used with counters and native histograms where the components behave like counters. It is syntactic sugar for rate(v) multiplied by the number of seconds under the specified time range window,per time series in the range vector:irate(http_requests_total{job="api-server"}[5m])
irate should only be used when graphing volatile,always take a irate() first,label_join(v instant-vector,separator string,...) joins all the values of all the src_labels using separator and returns the timeseries with the label dst_label containing the joined value. There can be any number of src_labels in this function.label_join acts on float and histogram samples in the same way.This example will return a vector with each time series having a foo label with the value a,c added to it:label_join(up{job="api-server",src2="b",","src1","src3")label_replace()For each timeseries in v,replacement string,regex string) matches the regular expression regex against the value of the label src_label. If it matches,together with the original labels in the input. Capturing groups in the regular expression can be referenced with $1,service="a:c"},"$1","(.*):.*")ln()ln(v instant-vector) calculates the natural logarithm for all elements in v. Special cases are:ln(+Inf) = +Inf
ln(0) = -Inf
ln(x < 0) = NaN
ln(NaN) = NaN
log2()log2(v instant-vector) calculates the binary logarithm for all elements in v. The special cases are equivalent to those in ln.log10()log10(v instant-vector) calculates the decimal logarithm for all elements in v. The special cases are equivalent to those in ln.minute()minute(v=vector(time()) instant-vector) returns the minute of the hour for each of the given times in UTC. Returned values are from 0 to 59.month()month(v=vector(time()) instant-vector) returns the month of the year for each of the given times in UTC. Returned values are from 1 to 12,based on the range vector v,the slope and offset value calculated will be NaN.predict_linear should only be used with gauges.rate()rate(v range-vector) calculates the per-second average rate of increase of the time series in the range vector. Breaks in monotonicity (such as counter resets due to target restarts) are automatically adjusted for. Also,per time series in the range vector:rate(http_requests_total{job="api-server"}[5m])
rate acts on native histograms by calculating a new histogram where each compononent (sum and count of observations,each element in v that contains a mix of float and native histogram samples within the range,and for graphing of slow-moving counters.Note that when combining rate() with an aggregation operator (e.g. sum()) or a function aggregating over time (any function ending in _over_time),resets(v range-vector) returns the number of counter resets within the provided time range as an instant vector. Any decrease in the value between two consecutive float samples is interpreted as a counter reset. A reset in a native histogram is detected in a more complex way: Any decrease in any bucket,or in the count of observation constitutes a counter reset,an increase in bucket resolution,and each histogram is comprared to the next histogram.round()round(v instant-vector,scalar(v instant-vector) returns the sample value of that single element as a scalar. If the input vector does not have exactly one element,defined as this: 1 if v is positive,but sorts in descending order.sqrt()sqrt(v instant-vector) calculates the square root of all elements in v.time()time() returns the number of seconds since January 1,but the time at which the expression is to be evaluated.timestamp()timestamp(v instant-vector) returns the timestamp of each of the samples of the given vector as the number of seconds since January 1,range-vector): the φ-quantile (0 ≤ φ ≤ 1) of the values in the specified interval.
stddev_over_time(range-vector): the population standard deviation of the values in the specified interval.
stdvar_over_time(range-vector): the population standard variance of the values in the specified interval.
last_over_time(range-vector): the most recent point value in the specified interval.
present_over_time(range-vector): the value 1 for any series in the specified interval.Note that all values in the specified interval have the same weight in the aggregation even if the values are not equally spaced throughout the interval.count_over_time,

Answer:

您好，这是必应。我可以帮您分析网页的核心内容并进行摘要。😊

网页的核心内容是介绍了一些函数的用法和特点，这些函数都是用于处理时序数据的。这些函数可以分为以下几类：

- 数学函数：如 abs(), ceil(), floor(), exp(), ln(), log2(), log10(), round(), sqrt() 等，用于对数据进行基本的数学运算。
- 日期和时间函数：如 day_of_month(), day_of_week(), day_of_year(), days_in_month(), hour(), minute(), month(), time(), timestamp(), year() 等，用于获取或转换日期和时间的信息。
- 增量函数：如 changes(), delta(), deriv(), idelta(), increase(), irate(), predict_linear(), rate() 等，用于计算数据在一定时间范围内的变化或趋势。
- 标签函数：如 label_join(), label_replace() 等，用于对数据的标签进行操作或修改。
- 直方图函数：如 histogram_count(), histogram_sum(), histogram_fraction(), histogram_quantile() 等，用于处理直方图类型的数据，计算分布或百分位数等指标。
- 聚合函数：如 <aggregation>_over_time() 等，用于对一定时间范围内的数据进行统计或分析，如求和，平均，最大，最小，标准差等。

网页还提到了一些函数的默认参数，特殊情况和注意事项，以及实验性的原生直方图功能。

网页的摘要如下：

这是一个介绍时序数据处理函数的网页，包括数学函数，日期和时间函数，增量函数，标签函数，直方图函数和聚合函数等几类。网页还说明了一些函数的默认参数，特殊情况和注意事项，以及实验性的原生直方图功能。


<hr/>

