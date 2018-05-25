# Prometheus @backend

---

## What is Prometheus?

+++

Prometheus is an open-source systems monitoring and alerting toolkit base on purely numeric time series.
<br>
<br>
"Cloud Native Computing Foundation" member project
<br>
<br>
https://prometheus.io

+++

### Why Prometheus?

> a single big Prometheus server can easily store millions of time series, with a record of 800,000 incoming samples per second [...]. Given a 10-seconds scrape interval and 700 time series per host, this allows you to monitor over 10,000 machines from a single Prometheus server.

<span style="font-size:0.6em;">https://prometheus.io/blog/2016/07/23/pull-does-not-scale-or-does-it/#it-doesn-t-matter-who-initiates-the-connection</span>

+++

#### Very flexible multi dimensional data model

---

## Concepts

+++

### Timeseries

Stream of samples of the same metric and the same set of labels

#### Sample
- a float64 value
- a millisecond-precision timestamp

+++

### Scraping (Pulling)

Pulling metrics via HTTP (aka scraping)

#### Why Pull?
- Simple client implementation
- No client configuration
- No performance overhead on the client as they only update counters
- Easy debugging on the client (with your browser)
- Immediately notice when a target is down

+++

#### Events vs. state
Prometheus collects the state and not single events (like the count of http requests and not the single requests).

---

## Metric Types
- Counter
- Gauge
- Histogram
- Summary

+++

### Counter

##### a single numerical value that only ever goes up
##### Counter resets are handled by the server

+++

### Gauge

##### a single numerical value that can arbitrarily go up and down.

+++

### Histogram

##### samples observations (usually things like request durations or response sizes) and counts them in configurable buckets

+++

### Summary

##### summaries calculate streaming φ-quantiles on the client side

+++

TODO: Explain Histogram buckets

---

## What shall I measure?

+++

### The Four Golden signals
##### Latency, Traffic, Errors, Saturation

<span style="font-size:0.6em;">https://landing.google.com/sre/book/chapters/monitoring-distributed-systems.html</span>

+++

### Latency
##### The time it takes to service a request.
##### Distinguish between GET and POST and successful and failed requests

+++

### Traffic
###### HTTP requests per second

+++

### Error
The rate of requests that fail (500s)

+++

### Saturation
##### How "full" your service is.
