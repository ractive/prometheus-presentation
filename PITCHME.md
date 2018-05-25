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
[a float64 value, a millisecond-precision timestamp]

+++

### Scraping (Pulling)

Pulling metrics via HTTP from /metrics

+++

#### Why Pull?
- Simple client implementation
- No client configuration
- No performance overhead on the client as they only update counters
- Easy debugging on the client (with your browser)
- Immediately notice when a target is down

+++

#### Events vs. state
Prometheus collects the *state* and *not single events* (like the count of http requests and not the single requests).

---

## Metric Types

+++

##### Counter
##### Gauge
##### Histogram
##### Summary

+++

### Counter

A single numerical value that only ever goes up

+++

### Gauge

A single numerical value that can arbitrarily go up and down.

+++

### Histogram

Samples observations (usually things like request durations or response sizes) and counts them in configurable buckets

+++

### Summary

Summaries calculate streaming φ-quantiles on the client side

+++

TODO: Explain Histogram buckets

---

## What shall I measure?

+++

### The Four Golden signals
Latency, Traffic, Errors, Saturation
<br>
<br>
<span style="font-size:0.6em;">https://landing.google.com/sre/book/chapters/monitoring-distributed-systems.html</span>

+++

### Latency
The time it takes to service a request.
<br>
<br>
Distinguish between GET vs. POST and successful vs. failed requests.

+++

### Traffic
HTTP requests per second

+++

### Error
The *ratio* of requests that fail (500s)

+++

### Saturation
How "full" your service is.

---

## Timeseries

+++

### Metric Naming 

`<namespace>_<subsystem>_my_metric_name_<unit>`<br>
<br>
`backend_http_requests_total` (with `backend` as namespace)<br>
`backend_auth_authentication_success_total` (with `backend` as namespace and `auth` as subsystem)

+++

Use base units (seconds, not milliseconds)
<br>
<br>
Add a suffix describing the unit
`backend_http_response_time_seconds`<br>
`backend_http_requests_total`<br>
`process_cpu_seconds_total`<br>

<span style="font-size:0.6em;">https://prometheus.io/docs/practices/naming/</span>

+++

### Labels

Differentiate the characteristics of the thing that is being measured<br>
<br>
`backend_http_requests_total{method="GET", path="/users", app="user-service"}`<br>
`backend_auth_users_activated_total{platform="Android"}`<br>
<br>
<span style="color: red">Remember that every unique combination of key-value label pairs represents a new time series</span>



