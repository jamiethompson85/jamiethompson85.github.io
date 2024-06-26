---
layout: post
title: Simplifying data ingestion with Google Cloud's Pub/Sub BigQuery Subscriptions
subtitle: In this blog I cover how to implement a simple data ingestion pipeline using Google Cloud Pub/Sub's BigQuery Subscription service including example Terraform code.
#cover-img: /assets/img/path.jpg
#thumbnail-img: /assets/img/gcpdiag/gcpdiag-stethoscope.png
#share-img: /assets/img/gcpdiag/gcpdiag-stethoscope.png
readtime: true
share-title: "Simplifying data ingestion with Google Cloud's Pub/Sub BigQuery Subscription"
share-description: "In this blog I cover how to implement a simple data ingestionpipeline using Google Cloud's Pub/Sub BigQuery Subscription service including example Terraform code."
tags: [BigQuery Subscription, Pub/Sub, Data Ingestion, ELT]
---

* toc
{:toc}

# Google Cloud's Pub/Sub BigQuery Subscriptions
Google Cloud's Pub/Sub BigQuery subscriptions simplify data ingestion pipelines that require little or no data transformation. Applications performing extract, load and transform (ELT) tasks no longer need to make use of Cloud Functions or Dataflow to subscribe to a Pub/Sub topic and load data into BigQuery. Instead, Pub/Sub BigQuery subscriptions send messages directly to BigQuery as they are received.

![Pub/Sub BigQuery Subscription](/assets/img/bigquerysub/pubsub-bigquery-subscription.png "Pub/Sub BigQuery Subscription")
 
***Pub/Sub BigQuery Subscription Architecture***

Messages are sent to BigQuery in one of two ways. The default method loads the messages in their raw format, into the BigQuery table under a data column/field for later manipulation.

![BigQuery Subscription Default Data Ingestion Format](/assets/img/bigquerysub/pubsub-subscription-raw-data-column.PNG "BigQuery Subscription Default Data Ingestion Format")
 
*Example BigQuery Subscription Default Data Ingestion Format*

Alternatively, a schema can be configured on the Pub/Sub Topic to define the format of message fields. The Piub/Sub BigQuery Subscription then uses this schema to load the defined message fields into the corresponding BigQuery table fields. 


![BigQuery Subscription With Schema Data Ingestion Format](/assets/img/bigquerysub/pubsub-subscription-with-schema-format.PNG "BigQuery Subscription with Schema Data Ingestion Format")
 
***Example BigQuery Subscription with Schema Data Ingestion Format***

In addition, metadata can be populated to help track information such as subscription name, message publish time etc. 



![BigQuery Subscription Schema Format with Metadata](/assets/img/bigquerysub/pubsub-subscription-schema-with-metadata.PNG "BigQuery Subscription Schema Format with Metadata")
 
***Example BigQuery Subscription Schema with Metadata Format***


With write additional metadata enabled, the BigQuery schema needs to have the following fields defined. However, these fields must not be defined within the Topic schema itself. 

| Parameters        	| Value                                                                                                                                                                                                                    	|
|-------------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| subscription_name 	| STRING Name of a subscription.                                                                                                                                                                                      	|
| message_id        	| STRING ID of a message                                                                                                                                                                                              	|
| publish_time      	| TIMESTAMP The time of publishing a message.                                                                                                                                                                         	|
| data              	| BYTES, STRING, or JSON The message body. The data field is required for all destination BigQuery tables that don't select Use topic schema. If the field is of type JSON, then the message body must be valid JSON. 	|
| attributes        	| STRING or JSON A JSON object containing all message attributes. It also contains additional fields that are part of the Pub/Sub message including the ordering key, if present.                                     	|


***BigQuery Subscription Metadata Fields/Columns***

If a message is received with additional fields not defined within the schema, BigQuery subscriptions can be configured to drop the message. If the BigQuery subscription doesn't enable drop unknown fields, the messages with extra fields remain in the subscription backlog. The subscription will then end up in an errored state.

To mitigate this, Pub/Sub Topic schemas should be configured to automatically drop unknown fields. This ensures the data is still written to BigQuery, but any additional message fields not defined within the schema are dropped.

Once data is loaded into BigQuery, simple SQL transformations can be performed on the raw data. With BigQuery scheduled queries, you can automate SQL transformation tasks based on a cron schedule you define.

Pub/Sub BigQuery subscriptions also remove the requirement to have Pub/Sub Topic clients configured as subscribers. The Pub/Sub BigQuery Subscription defines the BigQuery table data will be loaded into and is automatically pushed directly to BigQuery.

Messages target the BigQuery Write API- upon successful write to the BigQuery table, the Pub/Sub message is ackowledged. If the message fails to be written to the table, it is negatively acknowledged to Pub/Sub and Pub/Sub will attempt to write the data to BigQuery again. By configuring an exponential backoff, Pub/Sub will wait the defined amount of time before attempting to write a previously failed message, incrementing the wait period until it reaches the defined threshold for failed delivery attempts. Once this threshold has been met, the message is forwarded to a Dead Letter queue for manual review and intervention. The messages sent to the Dead Letter Queue include an additional CloudPubSubDeadLetterSourceDeliveryErrorMessage attribute which defines the reason the message couldn't be written to BigQuery.

# What IAM permissions do Pub/Sub BigQuery Subscriptions require?
The Pub/Sub service account requires write access to the BigQuery target table, and read access to the table metadata. These permissions can be granted by applying the following Terraform code. The google_bigquery_table_iam_member resource creates a non authoritative update to the IAM bindings, preserving any existing table bindings.

```
# grant pub/sub service account metadataViewer permissions on BigQuery target table
resource "google_bigquery_table_iam_member" "viewer" {
  dataset_id = google_bigquery_dataset.cloudbabbledataset01.dataset_id
  table_id = google_bigquery_table.cloudbabbletable01.table_id
  role   = "roles/bigquery.metadataViewer"
  member = "serviceAccount:service-${data.google_project.project.number}@gcp-sa-pubsub.iam.gserviceaccount.com"
}

# grant pub/sub service account dataeditor permissions on BigQuery target table
resource "google_bigquery_table_iam_member" "editor" {
  dataset_id = google_bigquery_dataset.cloudbabbledataset01.dataset_id
  table_id = google_bigquery_table.cloudbabbletable01.table_id
  role   = "roles/bigquery.dataEditor"
  member = "serviceAccount:service-${data.google_project.project.number}@gcp-sa-pubsub.iam.gserviceaccount.com"
}
```
***Code Example: Applying required permissions to BigQuery table with Terraform***


# Defining Pub/Sub Topic Schema
The Pub/Sub Topic schema defines the fields within the message that correspond to the columns within the BigQuery table. For this to work, the Topic Schema names and value types must match the BigQuery schema names and value types. Any optional fields within the Topic schema must also be optional within the BigQuery schema. However, required fields within the Topic schema do not need to be required within the BigQuery schema. If there are any fields within the BigQuery schema that are not present within the Topic schema, these fields must be in a nullable mode within the BigQuery schema.

```
resource "google_pubsub_schema" "cloudbabbleschema01" {
  name = "cloudbabbleschema01"
  type = "AVRO"
  definition = "{\n  \"type\" : \"record\",\n  \"name\" : \"Avro\",\n  \"fields\" : [\n    {\n      \"name\" : \"Username\",\n      \"type\" : \"string\"\n    },\n    {\n      \"name\" : \"Age\",\n      \"type\" : \"int\"\n    },\n    {\n      \"name\" : \"ActiveMember\",\n      \"type\" : \"boolean\"\n    }\n  ]\n}\n"
}
```
***Code Example: Creating a Pub/Sub topic schema with Terraform***

Once you have defined the Pub/Sub schema, you can then create a Topic configured with the schema. This Topic will then only accept messages that adhere to the defined schema.

```
resource "google_pubsub_topic" "cloudbabbletopic01" {
  name = "cloudbabbletopic01"

  depends_on = [google_pubsub_schema.cloudbabbleschema01]
  schema_settings {
    schema = "projects/${data.google_project.project.number}/schemas/cloudbabbleschema01"
    encoding = "JSON"
  }
}
```
***Code Example: Creating a Pub/Sub topic with schema with Terraform***

# Creating BigQuery Subscription
The following Terraform code provisions a BigQuery subscription.

```

#create pub/sub bigquery subscription for defined topic
resource "google_pubsub_subscription" "cloudbabblesubscription01" {
  name  = "cloudbabblesubscription01"
  topic = google_pubsub_topic.cloudbabbletopic01.name

  bigquery_config {
    table = "${google_bigquery_table.cloudbabbletable01.project}.${google_bigquery_table.cloudbabbletable01.dataset_id}.${google_bigquery_table.cloudbabbletable01.table_id}"
    use_topic_schema = true
  }

  depends_on = [google_bigquery_dataset_iam_member.viewer, google_bigquery_dataset_iam_member.editor]
}
```
***Code Example: Creating a BigQuery subscription with Pub/Sub Topic Schema with Terraform***

# Configuring Dead Letter Topic
The following terraform code provides an example Dead Letter Topic configuration for messages that fail to write to BigQuery within the defined threshold for failed delivery attempts. 
```
# create dead letter topic
resource "google_pubsub_topic" "cloudbabble_dead_letter" {
  name = "cloudbabble-dead-letter"
}

#create pub/sub bigquery subscription for defined topic
resource "google_pubsub_subscription" "cloudbabblesubscription01" {
  name  = "cloudbabblesubscription01"
  topic = google_pubsub_topic.cloudbabbletopic01.name

  bigquery_config {
    table = "${google_bigquery_table.cloudbabbletable01.project}.${google_bigquery_table.cloudbabbletable01.dataset_id}.${google_bigquery_table.cloudbabbletable01.table_id}"
    use_topic_schema = true
  }

# configure dead letter policy
  dead_letter_policy {
    dead_letter_topic = google_pubsub_topic.cloudbabble_dead_letter.id
    max_delivery_attempts = 10
  }

```
***Code Example: Creating a Dead Letter Topic and Policy with Terraform***
