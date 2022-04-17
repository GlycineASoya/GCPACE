# Cloud Functions

* *Events* - an action in Cloud, which *triggers* a *function*
* *Triggers* - a way of respoding to an *event*
* *Functions* - the code, that is associated with and executes a *trigger* in repsonse to the *event*
* Limits:
  * Time out: Default: 1 min, max: up to 9 mins

## Environment

* Python 3
* Node.js 6
* Node.js 8

## Creation of Function

### Creation of Function Cloud Console

Console -> Cloud Function

Options:

* Function name
* RAM allocated: from 128MB to 2GB
* Trigger: HTTP, Cloud Pub/Sub, Cloud Storage
* Event Type
* Bucket
* Source of the function
* Runtime
* Source code
* Stage bucket
* Function in source code to execute

### Creation of Function Cloud SDK (Cloud Shell)

`gcloud functions deploy FUNCTION_NAME --runtime RUNTIME [--trigger-resource TRIGGER_RESOURCE --trigger-event TRIGGER_EVENT_OPTION] [--trigger-topic PUBSUB_TOPIC] [--trigger-http TRIGGER_HTTP_OPTION]` - creation of Function:

Options:

* `runtime` - one of runtimes above
* `trigger-resource` - bucket name associated with the trigger
* `trigger-event` - one of the following options:
  * `google.storage.object.finalize` - the bucket file is fully uploaded
  * `google.storage.object.delete` - the bucket file is deleted
  * `google.storage.object.archive` - the bucket file archived
  * `google.storage.object.metadataUpdate` - the bucket file is updated
* `trigger-topic` - Cloud Pub/Sub topic for the trigger
* `trigger-http`:
  * GET
  * POST (PUT)
  * DELETE
  * OPTIONS

`gcloud functions delete FUNCTION_NAME` - delete Function
