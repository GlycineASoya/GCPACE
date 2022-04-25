# Monitoring, Logging, Cost Management

## Monitoring

* Metric - defined measurement on a resource collected at regular intervals and returns aggregated value (min, max, average)
* To monitor metrics and retrieve logs on a Linux VM the agents:
  * Monitoring Agent:

  ```bash
  curl -sSO https://dl.google.com/cloudagents/install-monitoring-agent.sh
  sudo bash install-monitoring-agent.sh
  ```

  * Logging Agent

  ```bash
  curl -sSO https://dl.google.com/cloudagents/install-logging-agent.sh
  sudo bash install-logging-agent.sh --structured
  ```

* Agents send streams from resources, grouping data into regular-sized buckets of time is called *aligning*
* To have an alerting against a metric *Alerting Policy* has to be created
* Custom metrics start with `custom.googleapis.com/`
* Custom metrics are described by two ways:
  * [OpenCensus](https://opencensus.io/) - high-level monitoring API library
  * Stackdriver's Monitoring API - low-level monitoring, which can [be written](https://cloud.google.com/monitoring/custom-metrics/creating-metrics)
    * C#
    * GO
    * Java
    * Node.js
    * PHP
    * Python
* Custom metric attributes:
  * Unique name within the project
  * Project
  * Display name and description
  * Metric kind (gauge - metric at a point in time, delta - change over an interval, cumulative - accumulate values over an interval)
  * Metric labels
  * Monitored resources

## Logging

* Logs are retained for 30 days
* Configuring Log Sinks
  * Log Sink - log location for the futher export to:
    * BigQuery: Data Set - table based on log name and timestamp
    * Cloud Storage: Bucket - log type and data (`log_sink1/syslog/2022/04/25/`)
    * Cloud Pub/Sub: Topic - base64 encoded LogEntry - logname, timestamp, textPayload, resource properties (e.g. `type`, `instance_id`, `zone`, `project_id`)
    * Custom Destination: Another Project
  * Cloud Console -> Logging -> Exports -> Create Export:
    * Sink name
    * Sink service (one of above)
    * Sink destination (one of above)
* Viewing and filtering logs
  * Cloud Console -> Logging -> Logs
* Viewing message details
* Using Cloud Diagnostics
  * *Cloud Trace* - distributed tracing system, collects latency daya from applications, helps identify bottlenecks. Cloud Console -> Trace
  * *Cloud Debug* - application debugger for inspecting the state of a running program, allows to take snapshots of the state of an application. Enabled by default on App Engine, can be enabled for Compute Engine, GKE. Cloud Console -> Debugger

## GCP Status

* Can be found on [Google Cloud Platform Status](https://status.cloud.google.com/) card of GCP Console Dashboard
* Status colour:
  * Green - service up and running
  * Orange - service disruption

## Pricing Calculator

* [Link](https://cloud.google.com/products/calculator/)
* Estimate cost for resource usage
