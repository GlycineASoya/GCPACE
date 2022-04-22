# Cloud Pub/Sub

## Deployment

* Create *Topic* - structure where applications can send messages
* Create *Subscription* - queue which applications can read a message from a Topic
  * Pushed - subscription writes to an endpoint; URL is required
  * Pulled - application reads from a Topic
* Once message is read, Pub/Sub waits for acknowledge from the application, using *Acknowledgement Deadline*: 10 - 600 secs
* Retention period for a message is determined manually

### Cloud Pub/Sub Cloud Console

Cloud Console -> Cloud Pub/Sub -> Create Topic

Cloud Console -> Cloud Pub/Sub -> three dots of the Topic -> New Subscription

### Streaming data Cloud Pub/Sub

`gcloud pubsub topics create TOPIC_NAME` - creating Topic

`gcloud pubsub subscriptions create --topic TOPIC_NAME SUBSCRIPTION_NAME` - creating Subscription on a Topic

`gcloud pubsub topics publish TOPIC_NAME --message MESSAGE` - publish a message to a Topic

`gcloud pubsub subscriptions pull --auto-ack SUBSCRIPTION_NAME` - read a message from a Topic
