# GCP Cloud SDK (gcloud)

After local installation do initialization:
`gcloud init` - runs process of registering the Cloud SDK against Google Cloud Organization using authentication link, sets default:
    zone

Structure:
`gcloud` - main command
`compute` - group in the resource hierarchy
`instances` - resource
`create|list|etc` - action
`--OPTION |=VALUE` - option

## gcloud-wide Options

`--account` - overrides the default account
`--configuration` - specifies named configuration file, contains eky-value pair
`--flatten` - generates key-value record in case of key has multiple values
`--format` - specifies an output format, CSV, JSON, YAML, text, etc
`--help` - help message
`--project` - overrides default GCP Project
`--quiet` - disables interactive propmts
`--verbosity` - specifies the level of details in output messages:
    debug
    info
    warning
    error

## Cloud Engine

### VM creation

Creation multiple instances with the Region and Zone inherited after the Project:
`gcloud compute instances create INSTANCE_NAME1, INSTANCE_NAME2`

Creation of the instance specifying the zone
`gcloud compute instance create INSTANCE_NAME1 --zone ZONE1`

Creation of the instance specifying the machine type
`gcloud compute instance create INSTANCE_NAME1 --machine-type=MACHINE_TYPE1`

Creation of the instance specifying the Preemptible availability flag
`gcloud compute instance create INSTANCE_NAME1 --preemptible`

### Instance managing

Start instances
`gcloud compute instances start INSTANCE_NAME1 INSTANCE_NAME2 [--async]`

`--async` - shows information of VM start process

Stop instances
`gcloud compute instances stop INSTANCE_NAME1 INSTANCE_NAME2 --zone <zone1> [--async]`

Delete instances
`gcloud compute instances delete INSTANCE_NAME1 INSTANCE_NAME2 --zone ZONE1 [--async] [--delete-disks|--keep-disks |=all|DISK_NAME]`

### Snapshots

Create snapshot of a disk
`gcloud compute disks snapshot DISK_NAME --snapshot-names=SNAPSHOT_NAME`

Get list of snapshots
`gcloud compute snapshots list`

Get detailed information about snapshot
`gcloud compute snapshots describe SNAPSHOT_NAME`

### Disks

Create disk
`gcloud compute disks create DISK_NAME --source-snapshot=SNAPSHOT_NAME [--size=SIZE_IN_GB] [--type=DISK_TYPE]`

Get VM disk types list
`gcloud compute disk-types list`

### Images

Create image
`gcloud compute images create IMAGE_NAME`

Options:
`--source-disk` - using disk
`--source-image` - using image
`--source-image-family` - latest image version in the Family
`--source-snapshot` - using snapshot
`--source-uri` - image on web URI (bucket)
`--description` - specifies descriptino
`--labels` - specifies labels

Delete image
`gcloud compute images delete IMAGE_NAME`

Export image to Cloud Storage
`gcloud compute images export --destination-uri DESTINATION_URI --image IMAGE_NAME`

### Instance Groups and Templates

Create instance group template
`gcloud compute instance-template create INSTANCE_TEMPLATE [--source-instance SOURCE_OF_TEMPLATE]`

Delete instance group template
`gcloud compute instance-template delete INSTANCE_TEMPLATE`

Delete instance group
`gcloud compute instance-groups managed delete-instances INSTANCE_GROUP`

List templates
`gcloud compute instance-template list`

List instance groups
`gcloud compute instance-groups managed list-instances`

List instances in instance group
`gcloud compute instance-groups managed list-instances INSTANCE-GROUP`

### Getting information

List the instances
`gcloud compute instances list [--filter="zone:ZONE_NAME"]`

Project description
`gcloud compute project-info describe`

Get VM disk types list
`gcloud compute disk-types list`

Get VM machine types list
`gcloud compute machine-types list`

Get zones list
`gcloud compute zonez list`

### Options

`--boot-disk-size` - size of boot disk, from 10GB to 2TB
`--boot-disk-type` - can be checked by `gcloud compute disk-types list`. Depends on zone
`--labels` - KEY=VALUE pairs, same as AWS Tags
`--machine-type`, can be checked by `gcloud compute machine-types list`
`--preemptible` - Preemtible flag
`--filter="FIELD_NAME:NAME_OF_THE_RESOURCE"` - filters the output
`--limit` - limits the mumber of VMs listed
`--sort-by` - reorders the list

## Kubernetes Engine (GKE)

### Getting Information

`gcloud container clusters list` - lists names, basic info of all clusters

`gcloud container clusters describe CLUSTER_NAME [--zone=ZONE_NAME]` - get details of the cluster, such as client certificate, username, password
