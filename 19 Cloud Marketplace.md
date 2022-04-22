# Cloud Marketplace

* Previous title - Cloud Launcher
* Provides fully provisioned application templates to deploy without configuration
* Contains *applications* and *data sets*
* Options to deploy:
  * Name of Deployment
  * Zone
  * Machine Type (preconfigured)
  * Administrator email

## Deployment Manager

* Makes available to create your own solution configuration files
* Configuration files are YAML files
  * `name`, the name of the resource
  * `type`, the type of the resource, e.g. `compute.v1.instance`
  * `properties`, key-value pairs, specifies configuration parameters for the resource

Example:

```YAML
resources:
- type: compute.v1.instance
name: deployment-vm
properties:
  machine-type: MACHINE_TYPE_GOOGLE_API_URL
  zone: ZONE
  disks:
  - deviceName: boot
    type: PERSISTENT
    boot: true
    autoDelete: true
```

`MACHINE_TYPE_GOOGLE_API_URL` = <https://www.googleapis.com/compute/v1/projects/[PROJECT_ID]/zones/us-central1-f/machineTypes/f1-micro> - Debian

### Deployment Manager Templates

* Templates are the files with Deployment configurations written either Python (complicated templates) or Jinja2
* Launching template: `gcloud deployment-manager deployments create quickstart-deployment --config vm.yaml`
* Describe a deployment: `gcloud deployment-manager deployments describe quickstart-deployment`
