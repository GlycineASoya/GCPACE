# Cloud App Engine

## Deploying App Engine Application

### Deploying Cloud SDK (Cloud Shell)

`gcloud components install APPLICATION_NAME` - install/update Python library as needed
`git clone GIT_URL` - downloads repository to the App Engine environment
`git app deploy YAML_FILE` - upload local config yaml and code to App Engine
`gcloud app versions stop APP_VERSION_NUMBER` - stops serving version

### YAML options

* `automatic_scaling:` - based on request rate, response latency, other app metrics
  * `target_cpu_utilization:` - threshold after which additional instances are started
  * `min_instances:`
  * `max_instances:`
  * `min_pending_latency:` - default value: 30ms. Indicates time in queue before proceed
  * `max_pending_latency:`
  * `target_throughput_utilization:` - maximum number of concurrent requests before add new instance. Value: 0.5..0.95
  * `max_concurrent_requests:` - maximum concurrent requests the instance can accept before starting new instance. Default: 10, max: 80
* `basic_scaling:` - based on application requests
  * `idle_timeout:`
  * `max_instances:`
* `manual_sclaing:` - allows to control scaling manually
  * `instances:` - set the number of the instances for the version of the service of the application

### Splitting traffic

* Done across versions
  * by IP address - client routes to the same split. App Engine creates a hash of IP address of each Version and number between 0..999
  * by HTTP cookie - assigning a user to a versions of the service. Best practice. App Engine uses HTTP request header `GOOGAPPUID` with a hash value between 0..999
  * by random selection - for even distribution workload

#### Google Cloud SDK (Cloud Shell)

`gcloud app service set-traffic SERVICE_NAME --splits SERVICE_VERSION1=0.0..1.0` - if no SERVICE_NAME specified - applied for all services
`gcloud app services set-traffic [--migrate] [--split-by]` - migration of the traffic. `migrate` indicates GAE should split traffic to the new version, `split-by` - how to split the traffic: `ip`, `cookie`, `random`
