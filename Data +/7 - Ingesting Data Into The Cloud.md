 
```
git clone https://github.com/GoogleCloudPlatform/data-science-on-gcp/
cd data-science-on-gcp
mkdir data
cd data
curl https://www.bts.dot.gov/sites/bts.dot.gov/files/docs/legacy/additional-attachment-files/ONTIME.TD.201501.REL02.04APR2015.zip --output data.zip
unzip data.zip
export PROJECT_ID=$(gcloud info --format='value(config.project)')
gsutil mb gs://${PROJECT_ID}-ml
bash ../02_ingest/ingest_from_crsbucket.sh ${PROJECT_ID}-ml


```