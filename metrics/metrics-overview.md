---
description: >-
  This guide describes the different types of evaluation metrics and how you can
  view them.
---

# Metrics Overview

For example, accuracy and mean squared errors are two common metrics for classification and regression, respectively.

Experiments, Deployments on Gradient can record metrics over the course of their execution. Spell will display these metrics on the Run page in the Spell web console.

We log three different kinds of metrics: hardware metrics, framework metrics, and custom user metrics.

### Hardware metrics <a id="hardware-metrics"></a>

All Gradient workloads like Experiments and Deployments monitor and track CPU, Memory, and Network. If the machine is equipped with a GPU, this will be tracked as well.

![System Metrics showing CPU and Memory Usage](../.gitbook/assets/screenshot-metrics.jpg)

### Framework metrics <a id="framework-metrics"></a>

If your deployment uses TF Serving, some metrics such as`tensorflow:core:direct_session_runs`, `tensorflow:cc:saved_model:load_attempt_count` etc. will be logged automatically.

### **User metrics**

You can log custom user metrics from inside of a experiment or deployment using the Python CLI utils. Its based on [prometheus Python Client](https://github.com/prometheus/client_python). Here's a trivial example:  


```python
from gradient_utils.metrics import 

logger = MetricsLogger(grouping_key={'ProjectA': 'SomeLabel'})

logger.add_gauge("Gauge")
logger.add_counter("Counter")


while datetime.now() <= endAt:
    randNum = randint(1, 100)
    logger["Gauge"] = 5
    logger["Gauge"].set(randNum)
    logger["Counter"].inc()
    logger.push_metrics()
```


