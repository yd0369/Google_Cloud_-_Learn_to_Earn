
```
gcloud iam service-accounts create my-sa-123 --display-name "my service account"


gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member serviceAccount:my-sa-123@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/editor

```


```
https://console.cloud.google.com/iam-admin/serviceaccounts

```

```
bigquery-qwiklab
```

```
BigQuery Data Viewer
```
```
BigQuery User
```

```
gcloud beta compute instances create bigquery-instance --zone=us-central1-a --machine-type=n1-standard-1 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=bigquery-qwiklab@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --image=debian-9-stretch-v20210916 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-balanced --boot-disk-device-name=bigquery-instance --reservation-affinity=any

gcloud beta compute ssh --zone "us-central1-a" "bigquery-instance"  --project $DEVSHELL_PROJECT_ID
```

-------------------------------------------------------

```
sudo apt-get update

sudo apt-get install virtualenv -y

virtualenv -p python3 venv

source venv/bin/activate

```

========================================================

```
sudo apt-get install -y git python3-pip

pip install google-cloud-bigquery

pip install pandas

echo "
from google.auth import compute_engine
from google.cloud import bigquery
credentials = compute_engine.Credentials(
    service_account_email='YOUR_SERVICE_ACCOUNT')
query = '''
SELECT
  year,
  COUNT(1) as num_babies
FROM
  publicdata.samples.natality
WHERE
  year > 2000
GROUP BY
  year
'''
client = bigquery.Client(
    project='YOUR_PROJECT_ID',
    credentials=credentials)
print(client.query(query).to_dataframe())
" > query.py


sed -i -e "s/YOUR_PROJECT_ID/$(gcloud config get-value project)/g" query.py

sed -i -e "s/YOUR_SERVICE_ACCOUNT/bigquery-qwiklab@$(gcloud config get-value project).iam.gserviceaccount.com/g" query.py

python query.py

```