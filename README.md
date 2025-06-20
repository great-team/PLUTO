# PLUTO Demonstration Code
Project Logistics, UTilization and Operations (PLUTO)
 
## Clone in the Repo
Open Cloud Shell\
Clone in the `https://github.com/ROIGCP/PLUTO` repo\
    Command: `git clone https://github.com/ROIGCP/PLUTO`\
    Command: `cd PLUTO`

## PLUTO dependancies
Make sure you have a project set\
    Command: `gcloud config set project YOURPROJECTNAME`

Bucket named projectid-bucket\
    Command: `gcloud storage buckets create gs://$GOOGLE_CLOUD_PROJECT-bucket`
    
BigQuery Dataset called "activities"\
    Command: `bq mk activities`

BigQuery Table called "resources" - starting schema\
    Command: `bq mk --schema messages:STRING -t activities.resources`

Enable the Pub/Sub APIs\
    Command: `gcloud services enable pubsub.googleapis.com`
    Command: `gcloud services list`

PubSub Topic called "activities"\
    Command: `gcloud pubsub topics create activities`

PubSub Subscription called "activites-catchall"\
    Command : `gcloud pubsub subscriptions create activities-catchall --topic=projects/$GOOGLE_CLOUD_PROJECT/topics/activities`

Create a Cloud Function\
    Python \
    Trigger by topic activities \
    Use the sample in CloudFunction folder

## Google Asset Managment examples

Enable the Asset Manager and Cloud Resource Manager APIs\
    Command: `gcloud services enable cloudasset.googleapis.com`\
    Command: `gcloud services enable cloudresourcemanager.googleapis.com`\
    Command: `gcloud services list`

Asset Export to BigQuery Example\
(NOTE: It make take a few minutes after API enablement for this command to work)\
    Command: `gcloud asset export --project=$GOOGLE_CLOUD_PROJECT --bigquery-table=export --bigquery-dataset=activities`

Asset Feed Creation (to Pub/Sub)\
    Command: 
    `gcloud asset feeds create activities --project=$GOOGLE_CLOUD_PROJECT --content-type=resource --asset-types="compute.googleapis.com.*" --pubsub-topic=projects/$GOOGLE_CLOUD_PROJECT/topics/activities`





