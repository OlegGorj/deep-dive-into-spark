# Metrics

## Overview


## Design and Implementation
### Spark Metrics System
![spark metrics](spark-metrics.png)


### Dropwizard Metrics

![dropwizard metrics](dropwizard-metrics.png)

`Metric` types:

* `Counter`: An incrementing and decrementing counter metric.
* `Gauge`: A gauge metric is an instantaneous reading of a particular value.
* `Metered`: An object which maintains mean and exponentially-weighted rate.
* `Histogram`: A metric which calculates the distribution of a value.
* `MetricSet`: A set of named metrics.