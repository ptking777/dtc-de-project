<h2>Google Compute Engine VM Instance</h2>
Setup Free account on Google Cloud.
https://cloud.google.com/free/

Setup Project and note the project ID.
https://developers.google.com/workspace/marketplace/create-gcp-project

Enable Billing for account. There will be no charges during the trial period.
https://cloud.google.com/billing/docs/how-to/manage-billing-account


<h2>Setup Google CLI</h2>

Download Google Access key: GOOGLE_APPLICATION_CREDENTIALS
https://cloud.google.com/docs/authentication/getting-started

Setup environment variable:
export GOOGLE_APPLICATION_CREDENTIALS=<path-to-directory>/.google/credentials/google_credentials.json


Install gcloud SDK on you local system.
https://cloud.google.com/sdk/docs/install

Execute the statement below and follow the instructions to authorize login from your local terminal:
gcloud auth login




<hr></hr>
<h1>Setup VM Instance</h1>

<h3>Set default compute zone</h3>
gcloud config set compute/zone us-central1-c


To display the current zone:

gcloud config get compute/zone
  us-central1-c

Create service account 'my-etl-worker' to be used by future applications and VM instances.
gcloud iam service-accounts create 'my-etl-worker' \
  --display-name='my-etl-worker'  \
      --description="My Service Account for ETL."

If you are successful, you should be able to see the new service account in the console:
https://console.cloud.google.com/iam-admin/serviceaccounts?project=<project_id>
my-etl-worker@<project-id>.iam.gserviceaccount.com

gcloud iam service-accounts describe my-etl-worker@dtc-de-zoom-camp.iam.gserviceaccount.com

Sample output:
    description: My Service Account for ETL.
    displayName: my-etl-worker
    email: my-etl-worker@dtc-de-zoom-camp.iam.gserviceaccount.com
    etag: MDEwMjE****=
    name: projects/dtc-de-zoom-camp/serviceAccounts/my-etl-worker@dtc-de-zoom-camp.iam.gserviceaccount.com
    oauth2ClientId: '10786490*****'
    projectId: dtc-de-zoom-camp
    uniqueId: '107864906*****'

Should you need to delete the service account:
    gcloud iam service-accounts delete my-etl-worker@dtc-de-zoom-camp.iam.gserviceaccount.com


To create a new private key for a service account, and save a copy of it locally, run the following command in your terminal:

gcloud iam service-accounts keys create my-etl-worker.json \
  --iam-account=my-etl-worker@dtc-de-zoom-camp.iam.gserviceaccount.com

Copy the my-etl-worker.json key file to a secure location. (.../.google/credentials/my-etl-worker.json)


Add IAM editor role to the service account.

gcloud iam service-accounts add-iam-policy-binding \
    my-etl-worker@dtc-de-zoom-camp.iam.gserviceaccount.com \
        --member='serviceAccount:my-etl-worker@dtc-de-zoom-camp.iam.gserviceaccount.com' --role='roles/editor'


Create a VM Instance using the terminal (either Cloud Shell or local terminal), execute the following:
<pre>
gcloud compute instances create my-etl-server --zone=us-central1-c \
    --machine-type=e2-medium \
    --image=ubuntu-2004-focal-v20220308 \
    --image-project=ubuntu-os-cloud \
    --boot-disk-size=100GB.  \
    --scopes='https://www.googleapis.com/auth/bigquery,https://www.googleapis.com/auth/datastore'
  
</pre>
NAME           ZONE           MACHINE_TYPE  PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP    STATUS<br>
my-etl-server  us-central1-c  e2-medium                  10.128.0.4   ????  RUNNING      <br>
<p>
<h2>Open firewalls for SSH and NiFI webserver</h2>
Get the IP address of your home computer using http://checkip.amazonaws.com/.
Also take note of the public IP address of the VM instance.   
<p>
Setup firewall rules to allow access to the NiFI server from your home IP. Execute the following from you home computer.
  
<pre>
export PORT=8443;
export MY_HOME_IP=???
export ETL_SERVER=my-etl-server
gcloud compute firewall-rules create rule-allow-tcp-${PORT} --source-ranges ${MY_HOME_IP} --target-tags allow-tcp-${PORT} --allow tcp:${PORT};
gcloud compute instances add-tags ${ETL_SERVER} --zone=us-central1-c --tags allow-tcp-${PORT};
</pre>
<p>
Repeat the above steps to allow SSH to the etl server from your home IP.
<pre>
export PORT=22;
export MY_HOME_IP=???
export ETL_SERVER=my-etl-server
gcloud compute firewall-rules create rule-allow-tcp-${PORT} --source-ranges ${MY_HOME_IP} --target-tags allow-tcp-${PORT} --allow tcp:${PORT};
gcloud compute instances add-tags ${ETL_SERVER} --zone=us-central1-c --tags allow-tcp-${PORT};
</pre>
<p>  
To authorize access to GCP resources from your home computer using the CLI, execute the statement below and login using using your GCP account in the browser window that will be displayed:
<br>    
gcloud auth login 
<br>
Now try to SSH into the ETL server using gcloud SDK:
gcloud compute ssh ${ETL_SERVER} --zone=us-central1-c  
<p>
Download the service account access key.  
<pre>
gcloud iam service-accounts keys create google_credentials.json \
    --iam-account=my-etl-worker@dtc-de-zoom-camp.iam.gserviceaccount.com   
 chmod 0400 ./google_credentials.json
 mkdir -p  /home/${USER}/.ssh/.google/credentials
 mv ./google_credentials.json /home/${USER}/.ssh/.google/credentials/google_credentials.json
  
Add the following line to ~/.bashrc 
  export GOOGLE_APPLICATION_CREDENTIALS=/home/<USER>/.ssh/.google/credentials/google_credentials.json
</pre>    
<p>
<h1>Google Cloud Storage Setup</h1>
From Google <a href="https://github.com/ptking777/dtc-de-project/blob/main/images/cloud_shell.png">Cloud Shell</a>, create bucket.
<pre>
gsutil mb gs://dtc_de_data_lake_ptk
</pre>
<p>
<h1>GCP BigQuery setup</h1>
From Goolge Cloud Shell, create dataset noaa_isd_analytics.
<pre>
bq --location=US mk -d \
--description "This is my dataset." noaa_isd_analytics
</pre>
<p>

  
  
  
  
  
  
  
